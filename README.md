
# Meeting Audio to Jira Ticket Pipeline

This pipeline takes an audio recording of a meeting, summarizes its content, and converts it into structured Jira tickets. It utilizes Instill AI's OpenAI and Groq components to analyze and format the summary, then creates Jira issues based on the extracted content.


Below is a demonstration of the pipeline in action:

https://github.com/user-attachments/assets/3efc358a-1004-4e69-acad-cefcff4118ff


## Pipeline Overview

### Components

1. **extract-and-summarize** (OpenAI Component)
   - Analyzes the meeting audio and provides a summary of the key insights.
   - Model: `whisper-1`
   - Steps:
     1. Summarizes the audio content.
     2. Extracts a title.
     3. Lists key insights.
     4. Identifies relevant keywords or tags.
     5. Suggests relevant locations if applicable.

2. **structure-response** (Groq Component)
   - Structures the summarized insights into a JSON format for Jira tickets.
   - Model: `llama3-8b-8192`
   - Response follows a specific JSON structure for Jira ticket creation.

3. **response-to-json** (Groq Component)
   - Validates and corrects JSON formatting to ensure compatibility with Jira.
   - Outputs structured JSON formatted strictly according to specified requirements.

4. **jira-ticket** (Jira Component)
   - Creates Jira tickets using the structured JSON data.
   - Populates ticket details like `summary`, `description`, `priority`, `assignee`, and tags.

### Variables

| Variable            | Description                      | Format           | UI Order |
|---------------------|----------------------------------|------------------|----------|
| `audio`             | Meeting audio recording         | audio           | 1        |
| `jira-project-key`  | Jira project key                | string          | 2        |
| `jira-email`        | Jira email ID                   | string          | 3        |
| `jira-base-url`     | Jira project base URL           | string          | 4        |

## Outputs

| Output          | Description                            |
|-----------------|----------------------------------------|
| `content`       | Summary of the audio content           |
| `groq-response` | Structured JSON response for Jira      |
| `result`        | Final JSON format for Jira ticketing   |

## Configuration Steps

1. **Set Up Secrets**
   - In your Instill project, add the following secrets:
     - `groq-api-key`: Your Groq API key for access.
     - `jira-api-key`: Jira API key for issue creation.

2. **Define Variables**
   - When running the pipeline, provide:
     - `audio`: Upload the meeting audio file.
     - `jira-project-key`: Jira project key (e.g., `PROJECT123`).
     - `jira-email`: Jira email ID.
     - `jira-base-url`: Jira project’s base URL (e.g., `https://yourcompany.atlassian.net`).

3. **Run the Pipeline**
   - Use the [Instill Pipeline Playground](https://instill.tech/anishagarwal20/pipelines/meeting-audio-to-jira-ticket/playground) to execute the pipeline with the provided variables.

## Example Usage

Upon execution, the pipeline will:
1. Extract and summarize the audio content.
2. Structure the information into JSON.
3. Generate Jira tickets for each key insight and add them to your specified project.

## Notes
- Ensure your Jira API key has the necessary permissions for issue creation.
- Refer to the [Instill Documentation](https://instill.tech) for detailed setup guidelines.
