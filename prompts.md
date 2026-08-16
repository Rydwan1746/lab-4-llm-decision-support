SUMMARY_PROMPT_V1 = "Summarize this loan application:\n\n{letter_text}"


SUMMARY_PROMPT_V2 = """You are an assistant to a microfinance loan officer. Your task is to summarize loan applications in a factual and neutral manner, without inventing any details. Please provide a concise summary in 3-4 sentences.
Summarize this loan application:{letter_text}"""


EXTRACT_PROMPT = """You are an assistant to a microfinance loan officer. Your task is to extract specific information from loan applications and return it in a structured JSON format. Please provide a JSON object with the following keys:
- applicant_name (string or null)
- amount_ghs (number or null)
- purpose (string or null)
- monthly_profit_ghs (number or null)
- has_collateral_or_guarantor (boolean or null)
- repayment_months (number or null)
If a field is not stated in the letter, use null. Do not guess.
Here is an example letter and the expected JSON output to guide you:
Letter: 
Dear Loan Officer,

My name is Abena Mensah and I am writing to apply for a loan of GHS 3,500 
to purchase additional sewing machines and fabric stock for my tailoring 
business located in Kumasi. I have been operating this business for four 
years and currently earn a monthly profit of approximately GHS 800. 

My neighbour, Mr. Kofi Darko, has agreed to serve as my guarantor for this 
loan. I would like to repay the loan over 12 months.

Thank you for your consideration.

Yours sincerely,
Abena Mensah

expected JSON: 
    {{
        "applicant_name": "Abena Mensah",
        "amount_ghs": 3500,
        "purpose": "to purchase additional sewing machines and fabric stock for my tailoring business located in Kumasi",
        "monthly_profit_ghs": 800,
        "has_collateral_or_guarantor": true,
        "repayment_months": 12
    }}
Now, extract the information from the following letter:{letter_text}
Return ONLY the JSON object, without any additional text or explanation."""


BRIEF_PROMPT = """You are an assistant to a microfinance loan officer. Your task is to provide a brief analysis of a loan application based on the letter and the extracted information. Please provide the following in your response:
1. Strengths (bullet points, grounded in the letter)
2. Risks / red flags (bullet points)
3. Missing information the officer should request
4. Suggested next step (e.g. "invite for interview", "request documents", "flag for senior review") — NOT "approve" or "reject".
Please ensure that your analysis is factual, neutral, and based solely on the information provided in the letter and the extracted data. Do not invent any details or make assumptions beyond what is explicitly stated. 
Final decisions are made by human officers. Here is the letter and the extracted information in JSON format:
Letter:{letter_text}
Extracted JSON:{extracted_json}
Return your analysis in a clear, structured format with numbered sections as specified above."""

