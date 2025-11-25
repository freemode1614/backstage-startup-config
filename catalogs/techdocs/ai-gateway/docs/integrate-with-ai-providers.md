# Integrations

> Securely store and manage AI provider credentials across your organization with centralized governance controls

<Note>
  Integrations are designed for **organization admins and managers** who need to manage AI provider access across teams. If you're looking to use AI models, see the [Model Catalog](/product/model-catalog) documentation.
</Note>

Integrations are the secure foundation for AI provider management in Portkey. Think of them as your organization's credential vault - a centralized place where you store API keys, configure access controls, and set usage policies that cascade throughout your entire AI infrastructure.

When you create an Integration, you're not just storing credentials - you're establishing a governance layer that controls:

* **Who** can access these AI services (through workspace provisioning)
* **What** models they can use (through model provisioning)
* **How much** they can spend (through budget limits)
* **How fast** they can consume resources (through rate limits)

## Why Integrations Matter

In enterprise AI deployments, raw API keys scattered across teams create security risks and make cost control impossible. Integrations solve this by:

1. **Centralizing Credentials**: Store API keys once, use everywhere through secure references
2. **Enabling Governance**: Apply organization-wide policies that automatically enforce compliance
3. **Simplifying Management**: Update credentials, limits, or access in one place
4. **Maintaining Security**: Never expose raw API keys to end users or applications
5. **Granular Observabilty**: Get complete end-to-end observability and track 40+ crucial metric for every single LLM call

## Creating an Integration

Let's walk through creating an Integration for AWS Bedrock as an example:

<Steps>
  <Step title="Navigate to Integrations">
    From your admin panel, go to **Integrations** and click **Create New Integration**.
  </Step>

  <Step title="Select Your AI Provider">
    Choose from 200+ supported providers. Each provider may have different credential requirements.

    <Frame>
      <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=df13f2b4eeb68e349b133a53344a543a" alt="Creating Bedrock Integration" data-og-width="2926" width="2926" data-og-height="1767" height="1767" data-path="images/product/model-catalog/integrations-page.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=870ae2d51d2735022e4446112c3037f5 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=7706d22e6f2e8c6079696182a937ac2e 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=977efcd287f8dd4e9efcd8762c8b139b 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=79dbdc82c6bb69529958682ff8b949b5 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=91822cf02bc1f3384b8fbf41b32d2add 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=d4a38499a77f6e46c48e91d30aa14c79 2500w" />
    </Frame>
  </Step>

  <Step title="Configure Integration Details">
    * **Name**: A descriptive name for this integration (e.g., "Bedrock Production")
    * **Slug**: A unique identifier used in API calls (e.g., "bedrock-prod")
    * **Description**: Optional context about this integration's purpose
    * **Endpoint Type**: Choose between Public or Private endpoints
  </Step>

  <Step title="Enter Provider Credentials">
    Each provider requires different credentials:

    **For OpenAI:**

    <Frame>
      <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=2cddcea37ed9d05c5a69759ce7f60268" alt="OpenAI Integration Setup" data-og-width="2527" width="2527" data-og-height="1676" height="1676" data-path="images/product/model-catalog/integrations-page-opnai.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=94806005afdfcc0e99725a8972c49f5d 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=214e6fdef5c578293f95bbcfcfb529ce 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=1ed9483e8e5eacb816c5068fc7270d2a 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=d7cb8f25efe129815eafe95d280f7093 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=ce07ca53f8f06ae4f3652dbb2990f895 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/integrations-page-opnai.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=c7d08ab5c5ad94b79a51b71e32cf4003 2500w" />
    </Frame>

    * API Key
    * Optional: Organization ID, Project ID

    **For AWS Bedrock:**

    * AWS Access Key
    * AWS Secret Access Key
    * AWS Access Key ID
    * AWS Region

    <Card href="/product/model-catalog/connect-bedrock-with-amazon-assumed-role" title="Connect Bedrock with Amazon Assumed Role">
      How to integrate Bedrock using Amazon Assumed Role Authentication
    </Card>

    Similarly for:

    * Azure OpenAI
    * Google Vertex AI
    * Anthropic
    * Gemini
      and more...
  </Step>
</Steps>

***

# Configuring Your Integration Access & Limits

After creating your Integration, you'll need to configure three key aspects that work together to control access and usage:

## 1. Workspace Provisioning

Workspace provisioning determines which teams and projects can access this Integration. This is crucial for maintaining security boundaries and ensuring teams only access approved AI resources.

#### How It Works

When you provision an Integration to a workspace:

1. That workspace can create AI Providers using this Integration's credentials
2. All usage is tracked at the workspace level for accountability
3. Budget and rate limits can be applied per workspace
4. Access can be revoked instantly if needed

#### Setting Up Workspace Provisioning

<Frame>
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=6e1a86e024e3c03a44d8d30152efbaaa" alt="Workspace Provisioning Configuration" data-og-width="2525" width="2525" data-og-height="1771" height="1771" data-path="images/product/model-catalog/workspace-provisioning-page.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=2d651857a8087684b685cb42fe524826 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=1ec67a5f93e500f7a41cfd1f77150d5e 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=7b3cb46a87d590f745f2c7ea4fa81584 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=1149b31104fa77ce31fce45cc3d9d0b8 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=422865620b72e123a9b2ff622ee5dee5 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/workspace-provisioning-page.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=1bba63504ebed8241452b41f0688c0ec 2500w" />
</Frame>

1. In your Integration settings, navigate to **Workspace Provisioning**
2. Select which workspaces should have access:
   * **All Workspaces**: Grants access to every workspace in your organization
   * **Specific Workspaces**: Choose individual workspaces that need access
3. For each workspace, click the `Edit Budget & Rate Limits` <Icon icon="pen-to-square" size={24} /> icon to configure:
   * Custom budget limits (see Budget Limits section below)
   * Custom rate limits (see Rate Limits section below)
   * Specific model access

#### Best Practices

* **Principle of Least Privilege**: Only provision to workspaces that genuinely need access
* **Environment Separation**: Create separate Integrations for dev/staging/production
* **Regular Audits**: Review workspace provisioning quarterly to remove unnecessary access

***

## 2. Model Provisioning

Model provisioning gives you fine-grained control over which AI models are accessible through an Integration. This is essential for:

* Controlling costs by restricting access to expensive models
* Ensuring compliance by limiting models to approved ones
* Maintaining consistency by standardizing model usage across teams

#### Setting Up Model Provisioning

<Frame>
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=dd617273c3e1cc352c5f1276631dc07c" alt="Model Provisioning Settings" data-og-width="2536" width="2536" data-og-height="1774" height="1774" data-path="images/product/model-catalog/model-provisioning-page.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=07c337093061bfc5a3ae2ad001a47ac7 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=83a6fc7326cda5b7e6b4fc764b9e0776 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=64c6b347c66ac2bd678e723aa607dc71 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=bd1d63a1106caa7991771408e03081af 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=b6f35f2aecc3c9681b97de0581065522 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/model-provisioning-page.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=48bc63b18b8f0fda0290d6b5b34a72b0 2500w" />
</Frame>

1. In your Integration settings, navigate to **Model Provisioning**
2. Select the configuration options:
   * **Allow All Models**: Provides access to all models offered by the provider
   * **Allow Specific Models**: Create an allowlist of approved models

#### Advanced Model Management

### Custom Models

The Model Catalog isn't limited to standard provider models. You can add:

* **Fine-tuned models**: Your custom OpenAI or Anthropic fine-tunes
* **Self-hosted models**: Models running on your infrastructure
* **Private models**: Internal models not publicly available

Each custom model gets the same governance controls as standard models.

<Card title="Custom Models" icon="wrench" href="/product/model-catalog/custom-models">
  Add and manage your fine-tuned, self-hosted, or private models
</Card>

### Overriding Model Details (Custom Pricing)

Override default model pricing for:

* **Negotiated rates**: If you have enterprise agreements with providers
* **Internal chargebacks**: Set custom rates for internal cost allocation
* **Free tier models**: Mark certain models as free for specific teams

Custom pricing ensures your cost tracking accurately reflects your actual spend.

<Card title="Custom Pricing" icon="tag" href="/product/model-catalog/model-overrides">
  Configure custom pricing for models with special rates
</Card>

***

## 3. Budget & Rate Limits

Budget and rate limits are configured within Workspace Provisioning and provide financial and usage guardrails for your AI operations.

<Frame>
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=a7debfad7682a196e68a8e30d6aa5a15" alt="Budget and Rate Limit Configuration" data-og-width="2523" width="2523" data-og-height="1763" height="1763" data-path="images/product/model-catalog/budget-and-limits-page-model-catalog.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=e05c75107157466242ecf6ecc52c5481 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=afb4d0ed0ff67fc42c1508e46fca887b 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=871a0c0994adfaebbd766d02d86bca1b 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=0a35b43925c94ccdaebe9416504bc48b 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=5e3bd7a92011f26930fe195b44375eaf 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/model-catalog/budget-and-limits-page-model-catalog.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=4d6f259dde1bbf75dbcee3e59efc1816 2500w" />
</Frame>

### Budget Limits

**Budget Limits on Integrations** provide a simple way to manage your spending on AI providers (and LLMs) - giving you confidence and control over your application's costs. They act as financial guardrails, preventing unexpected AI costs across your organization. These limits cascade down to all AI Providers created from this Integration.

#### Setting Budget Limits

1. In your Integration settings, navigate to **Workspace Provisioning**
2. Select which workspaces should have access:
   * **All Workspaces**: Grants access to every workspace in your organization
   * **Specific Workspaces**: Choose individual workspaces that need access
3. Click on the  `Edit Budget & Rate Limits` <Icon icon="pen-to-square" size={24} /> icon to edit the budget limits for the selected workspace
4. Set your desired budget Limits
5. Optionally, Select the `Apply to every workspace where this integration is enabled` checkbox to apply the same budget limits to all workspaces where this integration is enabled

#### Cost-Based Limits

Set a budget limit in USD that, once reached, will automatically expire the key to prevent further usage and overspending.

#### Token-Based Limits

Set a maximum number of tokens that can be consumed, allowing you to control usage independent of cost fluctuations.

> #### Key Considerations for Budget Limits
>
> * Budget limits can be set as either cost-based (USD) or token-based
> * The minimum cost limit you can set is **\$1**
> * The minimum token limit you can set is **100 tokens**
> * Budget limits apply until exhausted or reset
> * Budget limits are applied only to requests made after the limit is set; they do not apply retroactively
> * Once set, budget limits **cannot be edited** by any organization member
> * Budget limits work for **all AI provider** created on Portkey using the given **integration**

#### Alert Thresholds

You can now set alert thresholds to receive notifications before your budget limit is reached:

* For cost-based budgets, set thresholds in USD
* For token-based budgets, set thresholds in tokens
* Receive email notifications when usage reaches the threshold
* Continue using the key until the full budget limit is reached

#### Periodic Reset Options

You can configure budget limits to automatically reset at regular intervals:

<Frame>
  <img src="https://mintlify.s3.us-west-1.amazonaws.com/portkey-docs/images/product/periodic-reset.png" />
</Frame>

**Reset Period Options:**

* **No Periodic Reset**: The budget limit applies until exhausted with no automatic renewal
* **Reset Weekly**: Budget limits automatically reset every week
* **Reset Monthly**: Budget limits automatically reset every month

**Reset Timing:**

* Weekly resets occur at the beginning of each week (Sunday at 12 AM UTC)
* Monthly resets occur on the **1st** calendar day of the month, at **12 AM UTC**, irrespective of when the budget limit was set prior

### Rate Limits

Rate limits control the velocity of API usage, protecting against runaway processes and ensuring fair resource distribution across teams.

#### Setting Rate Limits

1. In your Integration settings, navigate to **Workspace Provisioning**
2. Select which workspaces should have access:
   * **All Workspaces**: Grants access to every workspace in your organization
   * **Specific Workspaces**: Choose individual workspaces that need access
3. Click on the  `Edit Budget & Rate Limits` <Icon icon="pen-to-square" size={24} /> icon to edit the rate limits for the selected workspace
4. Set your desired rate Limits
5. Optionally, Select the `Apply to every workspace where this integration is enabled` checkbox to apply the same rate limits to all workspaces where this integration is enabled

#### Configuration Options

**Limit Types:**

* **Request-based**: Limit number of API calls (e.g., 1000 requests/minute)
* **Token-based**: Limit token consumption rate (e.g., 1M tokens/hour)

**Time Windows:**
You can choose from three different time intervals for your rate limits:

* **Per Minute**: Limits reset every minute, ideal for fine-grained control
* **Per Hour**: Limits reset hourly, providing balanced usage control
* **Per Day**: Limits reset daily, suitable for broader usage patterns

> #### Key Considerations for Rate Limits
>
> * Rate limits can be set as either request-based or token-based
> * Time intervals can be configured as per minute, per hour, or per day
> * Setting the limit to 0 disables the virtual key
> * Rate limits apply immediately after being set
> * Once set, rate limits **cannot be edited** by any organization member
> * Rate limits work for **all providers** available on Portkey and apply to **all organization members** who use the virtual key
> * After a rate limit is reached, requests will be rejected until the time period resets

#### Use Cases for Rate Limits

* **Cost Control**: Prevent unexpected usage spikes that could lead to high costs
* **Performance Management**: Ensure your application maintains consistent performance
* **Fairness**: Distribute API access fairly across teams or users
* **Security**: Mitigate potential abuse or DoS attacks
* **Provider Compliance**: Stay within the rate limits imposed by underlying AI providers

#### Exceeding Rate Limits

When a rate limit is reached:

* Subsequent requests are rejected with a specific error code
* Error messages clearly indicate that the rate limit has been exceeded
* The limit automatically resets after the specified time period has elapsed

***

## Monitoring and Analytics

### Tracking Spending and Usage

You can track your spending, usage, and 40+ crucial metrics for any specific AI integration by navigating to the Analytics tab and filtering by the **desired key** and **timeframe**.

<Frame>
  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=82def1b2a3c3312c20341f620e1dbcb5" data-og-width="600" width="600" data-og-height="348" height="348" data-path="images/product/product-1.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=7b9fb1941665c5e305f1456c3a786d81 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=f27cf972eb4eb24bca35fc6b1fd3fe3a 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=29df4161669b7e21846c657ade6352e2 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=b9a8472b8803cfe5975bac7b02f49127 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=82f4bebeda68829de439fc601e5fecb3 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-1.png?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=69149d7d0a1e24a87d4de835c0d413e1 2500w" />
</Frame>
