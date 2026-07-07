# AI-Powered Interview Trainer

> A serverless, full-screen AI interview simulator powered by IBM watsonx Orchestrate. Designed to provide instant, rubric-based feedback on technical problem-solving and STAR-method behavioral questions.

---

## 🚀 Overview

This repository contains a premium, high-performance, single-page web interface for an enterprise-grade **AI Interview Trainer**. It connects directly to a deployed **IBM watsonx Orchestrate Agent** using a zero-server, client-side architecture optimized for instant loading and absolute user focus.

Instead of building a resource-heavy server-side stack, this project leverages IBM watsonx Orchestrate’s native layout mechanics. By embedding the official loader script and passing explicit configuration overrides directly to the window object, it transforms the standard chat bubble into an immersive, full-screen application.

## 🏗️ Architecture

```text
┌────────────────────────────────────────────────────────┐
│                   Browser Client                       │
│  ┌──────────────────────────────────────────────────┐  │
│  │               Full-Screen UI Layout              │  │
│  │  ┌────────────────────────────────────────────┐  │  │
│  │  │                                            │  │  │
│  │  │        IBM watsonx Orchestrate Embed       │  │  │
│  │  │          (Form: fullscreen-overlay)        │  │  │
│  │  │                                            │  │  │
│  │  └────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────┘  │
└───────────────────────────┬────────────────────────────┘
                            │ (Secure Handshake)
                            ▼
               ┌──────────────────────────┐
               │ IBM watsonx Orchestrate  │
               │      Backend Agent       │
               └──────────────────────────┘
```

## ✨ Key Optimization Features

* **Native Full-Screen Overlay (`fullscreen-overlay`):** Forces the embedded agent canvas to consume `100vw` and `100vh` dynamically, hiding the underlying browser container completely.
* **Instant-On Session (`openChatByDefault`):** Bypasses the traditional landing screen or click-to-open mechanics, plunging the candidate into an interactive mock interview immediately on page load.
* **Immersive UX Control (`hideCloseButton` & `showLauncher`):** Completely eliminates the floating bubble launcher and removes the minimize button. This prevents user navigation errors, avoiding broken states or dead white space.
* **Zero-Server Blueprint:** Running entirely via client-side JavaScript means the application incurs zero hosting compute costs, experiences zero cold-start latencies, and is highly secure against server-side vulnerabilities.

## 🧠 Evaluated Interview Domains
The backend agent is loaded with comprehensive rubrics to evaluate responses across four critical domains:
1. **C++ & Data Structures:** Arrays, pointers, STL, algorithmic complexity, and advanced graphs/trees.
2. **Full-Stack Web Development (MERN):** React optimization, Node.js architecture, MongoDB scaling, and REST APIs.
3. **System Design:** Scaling, load balancing, caching, and distributed architectures.
4. **Behavioral & Corporate Fit:** Adherence to the STAR method, conflict resolution, and enterprise alignment.

## 🛠️ Code Structure & Embedding Mechanism

The integration is driven by a programmatic injection of the asynchronous `wxoLoader.js` script coupled with a precise configuration block:

```html
<script>
  window.wxOConfiguration = {
    orchestrationID: "4e653383727b48058237b569ea5e1f1d_7ccb2a81-ecad-42ff-bb24-77b24eb99de1",
    hostURL: "https://us-south.watson-orchestrate.cloud.ibm.com",
    rootElementID: "root",
    deploymentPlatform: "ibmcloud",
    crn: "crn:v1:bluemix:public:watsonx-orchestrate:us-south:a/4e653383727b48058237b569ea5e1f1d:7ccb2a81-ecad-42ff-bb24-77b24eb99de1::",
    
    /* UI Experience Overrides */
    openChatByDefault: true,
    hideCloseButton: true,
    showLauncher: false,
    layout: { 
        form: "fullscreen-overlay" 
    },
    
    chatOptions: {
        agentId: "9b01faac-1f58-4514-a55f-b7e906bf17b1", 
        agentEnvironmentId: "299cbee1-9fec-408b-a7d4-587d9ae38234",
    }
  };

  setTimeout(function () {
    const script = document.createElement('script');
    script.src = `${window.wxOConfiguration.hostURL}/wxochat/wxoLoader.js?embed=true`;
    script.addEventListener('load', function () {
        // Initialize the chat natively
        wxoLoader.init();
    });
    document.head.appendChild(script);
  }, 0);                     
</script>
```

## ⚡ Deployment & Local Run Instructions

Because this frontend is compiled into a singular, streamlined static HTML file, deployment is trivial.

### Running Locally
1. Clone this repository or download the source directory.
2. Double-click `index.html` to execute directly in any modern browser.
