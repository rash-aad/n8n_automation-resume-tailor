# n8n Automation - Resume Tailor

This repository contains the JSON for the "Resume Tailor Workflow", an n8n automation designed to assist with job applications by generating tailored materials.

## Workflow Overview

The core of this project is the **Resume Tailor Workflow**. It functions as an automated "expert career coach and resume-tailoring assistant". It receives a user's resume and a specific job description, then uses a Google Gemini LLM to generate a comprehensive report to help with the application.

### Workflow Steps

1.  **Trigger (Webhook):** The workflow is initiated by a `POST` request to a unique webhook URL.
2.  **Inputs:** The webhook is configured to receive:
    * A binary file (the resume) attached to the `resumeFile` property.
    * A JSON body containing a `jobDescription` field.
3.  **Resume Parsing:** The "Extract from File" node reads the text content from the uploaded PDF resume.
4.  **AI Processing (Gemini):** The extracted resume text and the job description are sent to a "Basic LLM Chain" which is powered by a "Google Gemini Chat Model".
5.  **Generated Report:** The LLM is prompted to generate a report with three specific sections:
    * **Skills to Add:** Keywords and qualifications from the job description that are missing or under-emphasized in the resume.
    * **Tailored Cover Letter:** A professional cover letter written to match the resume and job description.
    * **Application Email Body:** A brief, professional email for submitting the application.
6.  **Output:** The workflow takes the generated text, converts it into a file named `Application_Materials.txt`, and sends this file back as the webhook's response.

## How to Use

1.  **Import:** Import the `Resume Tailor Workflow.json` file into your n8n instance.
2.  **Credentials:** Connect the "Google Gemini Chat Model" node to your own Google Gemini (PaLM) API credentials. The current workflow is configured but will require your specific API key.
3.  **Activate:** Activate the workflow to enable the webhook.
4.  **Execute:** Send a `POST` request (using a tool like cURL, Insomnia, or Postman) to the workflow's webhook URL. The request must be `multipart/form-data` and include:
    * A file field named `resumeFile` containing your PDF resume.
    * A text field named `jobDescription` containing the text of the job description.
5.  **Receive:** The API call will return the `Application_Materials.txt` file, which you can save and review.
