# Platform Usage FAQ Guide

This document addresses common questions regarding role responsibilities during new VP onboarding and daily platform usage, tailored to different user roles within the platform.  

**Applicable to**: `Platform Administrators`, `VP Administrators`, and Regular `Developers`.

---

## 1. If a new VP needs to use our platform, what should be done?

### ✅ **Platform Administrator**: Responsible for establishing the overall organizational structure and permission architecture.

- **create Workspace**  
Create a new workspace under the organization, and fill in basic information such as the workspace name, description (which should include a brief introduction of the VP using this workspace), and the designated VP administrator.


- **Configure basic policies.**  
  - Set the default model list (e.g., qwen-max, glm-4)
  - Configure default budget limit and rate limit (e.g., 500 requests per minute)

- **Assign VP Administrator**  
  Designate the VP’s business or technical lead as the "VP Administrator" and grant them management permissions.

> 📌 Note: Once a VP is created, it can generate its own independent API Key and access context, operating completely isolated from other VPs.

---

### ✅ **VP Administrator**: Responsible for internal configuration and member management within the VP.

- **Verify model integration status.**  
  Check whether the required models for the VP (e.g., Qwen, GLM series) have been integrated into the platform and configured in the current workspace.
If not integrated, please contact the Platform Administrator.
  - If the model has already been integrated, ensure that it is enabled for use in the current workspace.
  - If the model does not exist in the already integrated models, the Platform Administrator needs to configure the corresponding model and enable its usage in the current workspace.

- **Configure VP-level model parameters.**  
  Set default parameters (e.g., `temperature=0.7`, `max_tokens=2048`), with support for custom configuration based on specific use cases.

- **add member**  
  Invite administrators and members to the current workspace and assign roles:
  - **member**：Can invoke APIs, view logs, access Analytics, and generate and distribute API Keys.
  - **manager**：In addition to all permissions of a member, it also includes the ability to manage members, view logs, and adjust configurations.

- **Generate and distribute API Keys.**  
  Provide developers with a dedicated API Key for this VP, used for accessing platform services.

> 📌 Note: API Keys are bound to a specific VP and cannot be used across VPs, ensuring secure isolation.

---

### ✅ **Developer**: Responsible for application integration and service invocation.

- **Obtain the VP's API Key.**  
  Obtain the dedicated API Key for the VP from the VP management team.

- **Integrate the SDK or call the API.**  
  Use the official SDK or make direct HTTP requests to call the platform's APIs. For specific examples, refer to the relevant documentation.



## 2. If the workspace team wishes to integrate and use a new large model, what are the responsibilities of each role?

When the workspace team intends to integrate a large model that has not yet been configured on the platform—such as a newly released Qwen 3.5, DeepSeek, or a privately deployed model — the integration process requires collaboration across multiple parties. Below are the specific responsibilities and operational steps for each role.

---

### ✅ **Platform Administrator**: Responsible for approving the model integration request and configuring the service.

- **Receive the integration request**  
  Receive the "new model integration" request from the workspace administrator, which includes:
  - Model name and version (e.g., qwen3-72b)
  - Service URL (e.g., https://api.example.com/v1/chat/completions)
  - Authentication method (API Key / Bearer Token / Signature)
  - Whether private deployment is supported
  - Expected use cases

- **Evaluation and Approval**  
  - Verify that the service URL is accessible (recommended to test connectivity)
  - Review security policies (e.g., whether HTTPS is enforced, whether IP whitelisting is required)
  - Other relevant review checks

- **Configure the model service**  
  - Create a new model entry in the platform backend and fill in the service configuration
  - Set default parameters (e.g., max_tokens=4096, temperature=0.8)
  - Make the model available in the corresponding workspace

- **Notify the workspace administrator**  
  Notify the workspace administrator: the model has been ready and is now available for use in the workspace.

---

### ✅ **workspace Administrator**: Responsible for enabling the new model within the workspace.

- **Check the availability status of the model**  
  Log in to the control plane and check the `Model Catelog` page to confirm whether the new model has been deployed and is ready to use or not

- **Set the default configuration for the model within the workspace.**  
  - Set workspace-level default parameters.

- **Configure the model access policy.**  
  - Set access permissions (e.g., whether all developers are allowed to use the model)  
  - Enable rate limiting (e.g., maximum 100 calls per minute)  
  - Turn on call logging and monitoring

- **Notify the developers within the project.**  
 Inform the developers: the new model is ready and can now be used.

> 📌 Note: After the model is enabled, it is visible and callable only by members of this project, ensuring isolation between projects.

---

### ✅ **Developer**: Responsible for calling the new model in the application

- **Confirm model availability**  
  Obtain information from the project administrator to confirm that the new model has been enabled in the project.

- **Update the calling code to specify the new model name**  
  In the API request, update the `model` parameter to the new model name, for
  ```json
  {
    "model": "qwen3-72b",
    "messages": [{"role": "user", "content": "what is panda?"}]
  }


## 3. How to add a new platform administrator?

Adding a new platform administrator involves assigning the highest-level system permissions and must follow a strict security approval process. Below are the responsibilities and operational steps for each role involved.

---

### ✅ **Platform Administrator** (current administrator): Responsible for submitting the permission request and conducting the approval.

- **Receive the new administrator request**  
  The request for adding a new platform administrator is submitted by an existing platform administrator or security officer, including:

  - New administrator’s name and contact information
  - Reason for request (e.g., team expansion, increased operational workload)
  - Expected scope of permissions (full platform management rights)

- **Conduct security assessment**  
  - Verify the applicant’s identity and role alignment

- **Invite administrator account and assign role**  
  - Log in to the platform console and navigate to the "Users and Permissions" management page
  - Add a new user and fill in basic information
  - Assign the role as "Admin" (highest system privilege)
  - Optional: Configure login method (e.g., bind enterprise email, enable MFA)

- **Send notification and permission guidelines**  
  - Notify the new administrator via email
  - Provide initial login instructions and security usage guidelines
  - Emphasize: Platform administrators have global configuration rights, including model integration, project deletion, and system-level changes—high-risk operations

> 📌 Note: Exercise strict control and careful management when adding or maintaining administrator accounts.

---

### ✅ **Workspace Administrator**: No direct involvement required, but should be informed of changes

- **No action needed**  
  Project administrators do not participate in the process of adding new platform administrators.

- **Monitor permission change notifications**  
  If the change in platform administrators involves organizational restructuring or updates to permission policies, the platform administrator will send emails.

- **Contact the platform administrator for clarification if needed**  
  For example, to confirm whether project configuration permissions are affected or whether re-authorization is required.

---

### ✅ **Developer**: No involvement required, only need to stay aware of security alerts

- **No action needed**  
  Developers do not participate in the process of adding new platform administrators.

- **Stay vigilant and pay attention to security notifications**  
  If the platform issues a security alert (e.g., “new administrator added” or “permission change”), check whether it affects access to your project or data security.

- **Report suspicious activity immediately**  
  If unauthorized configuration changes, model deletion, or API key leaks are detected, notify the platform administrator right away.

---

<!-- ## Administrator management principle -->

| Role                    | added new platform administrator? | modified platform administrator permissions | deleted platform admin? |
| ----------------------- | --------------------------------- | ------------------------------------------- | ----------------------- |
| Platform Administrator  | ✅                               | ✅                                          | ✅                      |
| Workspace Administrator | ❌                               | ❌                                          | ❌                      |
| Developer               | ❌                               | ❌                                          | ❌                      |


---
