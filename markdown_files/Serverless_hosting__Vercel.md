---
title: "Serverless hosting: Vercel"
original_url: "https://tds.s-anand.net/#/vercel?id=serverless-hosting-vercel"
downloaded_at: "2025-06-12T14:51:41.144322"
---

[Serverless hosting: Vercel](#/vercel?id=serverless-hosting-vercel)
-------------------------------------------------------------------

Serverless platforms let you rent a single function instead of an entire machine. They’re perfect for small web tools that *don’t need to run all the time*. Here are some common real-life uses:

* A contact form that emails you when someone wants to hire you (runs for 2-3 seconds, a few times per day)
* A tool that converts uploaded photos to black and white (runs for 5-10 seconds when someone uploads a photo)
* A chatbot that answers basic questions about your business hours (runs for 1-2 seconds per question)
* A newsletter sign-up that adds emails to your mailing list (runs for 1 second per sign-up)
* A webhook that posts your Etsy sales to Discord (runs for 1 second whenever you make a sale)

You only pay when someone uses your tool, and the platform automatically handles busy periods. For example, if 100 people fill out your contact form at once, the platform creates 100 temporary copies of your code to handle them all. When they’re done, these copies disappear. It’s cheaper than running a full-time server because you’re not paying for the time when no one is using your tool - most tools are idle 95% of the time!

Rather than writing a full program, serverless platforms let you write functions. These functions are called via HTTP requests. They run in a cloud environment and are scaled up and down automatically. But this means you write programs in a different style. For example:

* You can’t `pip install` packages - you have to use `requirements.txt`
* You can’t read or write files from the file system - you can only use APIs.
* You can’t run commands (e.g. `subprocess.run()`)

[Vercel](https://vercel.com/) is a cloud platform optimized for frontend frameworks and serverless functions. Vercel is tightly integrated with GitHub. Pushing to your repository automatically triggers new deployments.

Here’s a [quickstart](https://vercel.com/docs/functions/runtimes/python). [Sign-up with Vercel](https://vercel.com/signup). Create an empty `git` repo with this `api/index.py` file.

To deploy a FastAPI app, add a `requirements.txt` file with `fastapi` as a dependency.

```
fastapiCopy to clipboardErrorCopied
```

Add your FastAPI code to a file, e.g. `main.py`.

```
# main.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello, World!"}Copy to clipboardErrorCopied
```

Add a `vercel.json` file to the root of your repository.

```
{
  "builds": [{ "src": "main.py", "use": "@vercel/python" }],
  "routes": [{ "src": "/(.*)", "dest": "main.py" }]
}Copy to clipboardErrorCopied
```

On the command line, run:

* `npx vercel` to deploy a test version
* `npx vercel --prod` to deploy to production

**Environment Variables**. Use `npx vercel env add` to add environment variables. In your code, use `os.environ.get('SECRET_KEY')` to access them.

### [Videos](#/vercel?id=videos)

[![Vercel Product Walkthrough](https://i.ytimg.com/vi_webp/sPmat30SE4k/sddefault.webp)](https://youtu.be/sPmat30SE4k)

[![Deploy FastAPI on Vercel | Quick and Easy Tutorial](https://i.ytimg.com/vi_webp/8R-cetf_sZ4/sddefault.webp)](https://youtu.be/8R-cetf_sZ4)

[Previous

Notebooks: Google Colab](#/colab)

[Next

CI/CD: GitHub Actions](#/github-actions)