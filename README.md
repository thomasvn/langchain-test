# chat.thomasvn.dev

[![Netlify Status](https://api.netlify.com/api/v1/badges/e0a803e1-861d-4f5f-89f0-e65771791719/deploy-status)](https://app.netlify.com/sites/thomasvn/deploys)

## Demo

<https://chat.thomasvn.dev>

![Demo of chat.thomasvn.dev](./demo.png)

## Setup

Deploying the GCP Cloud Run Funciton:

```sh
gcloud functions deploy thomasvn-chat \
  --gen2 \
  --runtime=go122 \
  --region=us-west1 \
  --source=. \
  --entry-point=Chat \
  --trigger-http \
  --allow-unauthenticated \
  --memory=128Mi \
  --cpu=.083 \
  --env-vars-file=.env.yaml

gcloud functions describe thomasvn-chat --region=us-west1
gcloud functions delete thomasvn-chat --region=us-west1
```

Local Testing:

```sh
export OPENAI_API_KEY=""
export OPENAI_MODEL="gpt-4o-mini"
go run pkg/cmd/main.go "What has Thomas written about regarding Formula1?"
```

## References

- OpenAI Models (GPT-4o mini recommended)
  - <https://platform.openai.com/docs/models>
- LangChain
  - <https://github.com/tmc/langchaingo>
- Google Cloud Run Function v2
  - <https://cloud.google.com/functions/docs/create-deploy-http-go>
  - <https://github.com/GoogleCloudPlatform/functions-framework-go>

<!-- 
IDEAS
- Logging of what chats are being sent.
- Actual chat functionality. Ability to go back and forth with messages.
- Move GoogleCloudFunction into its own package? Would that still work?
- Pull contents of all Kubecost codebases & docs
- Build as a serverless container?
- https://www.val.town/
-->

<!-- 
DONE (most recent to least recent)
- Better prompting. Return chat as "Thomas" and talk in Thomas's voice.
- Enhance responses provided by OpenAI. Give the bot the ability to extrapolate. Custom prompt. GPT4o mini.
- Translate the HTML docs to Markdown. Reduces tokens.
- Deploy `chat.thomasvn.dev` site via Netlify
- Google Cloud Function v2. Deploy via API. Restructure code. https://cloud.google.com/functions/docs/create-deploy-http-go
- Expose it as an API via GCP Cloud Functions
- Graceful failure when cloning the repo
- Questions are parameterized and passed as CLI Args
-->
