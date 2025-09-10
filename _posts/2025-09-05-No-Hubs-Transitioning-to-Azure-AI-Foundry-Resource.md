---
title: "(I Don't Want) No Hubs: Transitioning from Azure AI Hubs to the new Azure AI Foundry resource"
date: 2025-09-05
layout: post
image: /assets/images/2025-09-05-No-Hubs-Transitioning-to-Azure-AI-Foundry-Resource/compare-project-structure.png
---

# **(I Don't Want) No Hubs**: Transitioning from Azure AI Hubs to the new Azure AI Foundry resource

*Demystifying the new experience for Azure AI Hub and Azure AI Services users*

---

![Foundry projects simplify initial setup and reduce the number of discrete services required to get started. Image from https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/migrate-project?tabs=azure-ai-foundry](/assets/images/2025-09-05-No-Hubs-Transitioning-to-Azure-AI-Foundry-Resource/compare-project-structure.png)

## Introduction

Azure AI Foundry has [introduced a new Azure resource](https://learn.microsoft.com/en-us/azure/ai-services/multi-service-resource?context=%2Fazure%2Fai-foundry%2Fcontext%2Fcontext&pivots=azportal) that changes how teams build, deploy, and manage generative AI applications at scale. If your organization has been working with hub-based projects and are planning to take your Azure AI Agents into production, you should consider shifting to the new Azure AI Foundry resource model.

In this post, we will walk through the technical differences between the AI Foundry resource and Azure AI Hubs, and offer guidance for teams planning their migration.

---

## Why the change in the first place?

Previously, infusing AI into applications took more of a modular approach, and generally only required resources specific to the task. An example of this could be the creation of Azure Machine Learning resource to add a scoring model to a web app, followed by the creation of a Computer Vision resource to enable image classification.

With the advent of generative AI, expectations have shifted towards complex AI apps requiring multiple models and modalities right out of the gate. The move from hub-based to Foundry projects reflects Microsoft’s objective of catering to these evolved expectations via a **unified platform-as-a-service for enterprise AI**. 

With the new Azure AI Foundry Resource, Microsoft consolidates these capabilities into a single, enterprise-grade resource that simplifies development, enhances governance, and improves scalability.

![Simplifying access to Azure AI via Foundry is valuable as baseline Enterprise Azure AI Apps grow more complex. Image from https://learn.microsoft.com/en-us/azure/architecture/ai-ml/architecture/baseline-azure-ai-foundry-chat](/assets/images/2025-09-05-No-Hubs-Transitioning-to-Azure-AI-Foundry-Resource/baseline-ai-app-arch.png)

---

## What's Different: AI Hub

If you have been building with [Azure AI Hubs](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-resources), the biggest difference you'll notice when moving to AI Foundry is that there are fewer resources created at startup. This is because Azure AI Hubs are based off [Azure Machine Learning](https://azure.microsoft.com/en-us/products/machine-learning/?msockid=199a3d1800c5654634e3293d01a064f8) *(you might have noticed you can open your AI Hub in ML Studio!)* and inherit some of the same dependencies of AML, namely a [Storage Account and Key Vault](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-resources#storage-and-key-vault-dependent-resources). Creating an Azure AI Hub also creates an Azure AI Foundry Resource, which acts as the Hub's library to access AI models. 

In contrast, creating an instance of a Foundry resource directly results in a single Azure resource, with features like RBAC, networking, and policy applied against the single resource. This also includes access to a central [Foundry API and SDK](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/develop/sdk-overview?tabs=sync&pivots=programming-language-python) for accessing multiple types of AI models simultaneously. This simplifies the experience for both developers and IT admins.

![Deploying an Azure AI Foundry resource results in fewer line items than an AI Hub; interestingly, an Azure AI Foundry resource is also among the services deployed along with the AI Hub!](/assets/images/2025-09-05-No-Hubs-Transitioning-to-Azure-AI-Foundry-Resource/compare-deployed-resources.png)

While AI Foundry resources are the default choice moving forward, that doesn't mean it is *always* the answer when planning a project. There are still some features from hub-based projects that have not made their way to Foundry projects, the most notable being [open source model deployments](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-use-foundation-models?view=azureml-api-2) and [Prompt Flows](https://learn.microsoft.com/en-us/azure/machine-learning/prompt-flow/overview-what-is-prompt-flow?view=azureml-api-2). If your projects require this, you may need to stick with hub-based projects a little longer, and monitor [AI Foundry product updates](https://learn.microsoft.com/en-us/azure/ai-foundry/whats-new-azure-ai-foundry) to determine your ideal migration date.

To close out this segment, here's a summary of key technical differences between the two, as well as capability differences as of September 5, 2025.

### Key Technical Differences

| Feature | Hub-Based Projects | Foundry Projects |
|---------|--------------------|------------------|
| Resource Model | Requires Hub + Foundry resources and dependencies | Single Foundry resource |
| Project Structure | Projects grouped under Hubs | Projects are child resources of Foundry |
| Model Access | Azure OpenAI + ML Studio | Unified access to Azure OpenAI, Meta, Mistral |
| Governance | Shared settings via Hub | Centralized RBAC, networking, and policy control at resource level |

### [Capabilities Comparison](https://learn.microsoft.com/en-us/azure/ai-foundry/what-is-azure-ai-foundry#which-type-of-project-do-i-need)

| Capability                                                                 | Azure AI Foundry project         | Hub-based project                                 |
|----------------------------------------------------------------------------|----------------------------------|---------------------------------------------------|
| Agents                                                                     | ✅ (GA)                          | ✅ (Preview only)                                |
| AI Foundry API to work with agents and across models                       | ✅ (Native support)              | Available via connections                        |
| Models sold directly by Azure - Azure OpenAI, DeepSeek, xAI, etc.          | ✅                               | Available via connections                         |
| Partner/Community Models sold via Marketplace - Stability, Bria, etc.      | ✅                               | Available via connections                         |
| Open source models such as HuggingFace                                     |                                  | ✅                                                |
| Evaluations                                                                | ✅                               | ✅                                                |
| Playground                                                                 | ✅                               | ✅                                                |
| Prompt flow                                                                |                                  | ✅                                                |
| Content understanding                                                      | ✅                               | ✅                                                |
| Project files (directly upload files and start experimenting)              | ✅                               |                                                   |
| Project-level isolation of files and outputs                               | ✅                               | ✅                                                |
| Required Azure dependencies                                                | -                                | Azure Storage account, Azure Key Vault            |

---

## What's Different: Azure AI Services

It's worth including Azure AI Services and its evolution here, as there may still be some of you who remember the Azure Cognitive Services Multi-Service Account. 

Before generative AI was widely available, Microsoft's Cognitive Services provided cutting-edge AI models that enabled computers to understand speech, images, language + intent, and documents. They were offered as discrete services, each with their own billing models. The Cognitive Services Multi-Service Account offered a way for developers to gain access to all of these models using one key, and serves as a great parallel for the current Azure AI Foundry resource transformation.

Cognitive Services was eventually renamed to **Azure AI Services**, and a new Azure AI Services resource was announced with it. This resource offered simplified access to the same Cognitive Services, but also included generative AI models like Azure OpenAI. **Azure AI Services have since gone through one more evolution and are now the Azure AI Foundry Resource**, with new capabilities including the AI Foundry API and project capabilities that allow it to replace hub-based projects.

---

## Migrating from hub-based projects to Foundry projects

Now that we have the context and understand the features that may make Foundry projects your best way forward, we need to plan for migration.

Fortunately, since an AI Hub already includes the creation of a Foundry resource in its provisioning, migration can be as simple as creating your hub-based projects in the Foundry resource and continuing from there. However, there may be some external connections (Azure AI Search, external DBs, etc.) that should be recreated; you can [review the full guide in the official Microsoft docs](https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/migrate-project?tabs=azure-ai-foundry).

If you're just getting started with Azure AI Foundry, you can alternatively [consult this guide to help plan for your networking, security, and user access requirements](https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/planning).

---

## Conclusion

The Azure AI Foundry Resource represents a simplified approach to engaging with Microsoft’s robust AI platform and offerings, and offers an essential building block for building AI-native applications.

Whether you're just getting started or already knee-deep in hub-based projects, I hope this guide provides clarity to differentiate between the two approaches and identify which model is best for you.

---

Thanks for reading, and Happy Building!

![Happy Building](/assets/images/happy-building.png)