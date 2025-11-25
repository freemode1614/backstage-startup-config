# Logs

> The Logs section presents a chronological list of all the requests processed through Portkey.

<Info>
  This feature is available for all plans:

  * [Developer](https://app.portkey.ai/): 10k Logs / Month with 3 day Log Retention
  * [Production](https://app.portkey.ai/): 100k Logs / Month + \$9 for additional 100k with 30 Days Log Retention
  * [Enterprise](https://portkey.ai/docs/product/enterprise-offering): Unlimited
</Info>

Each log entry provides useful data such as the timestamp, request type, LLM used, tokens generated, thinking tokens and cost. For [multimodal models](/product/ai-gateway/multimodal-capabilities), Logs will also show the image sent with vision/image models, as well as the image generated.

By clicking on an entry, a side panel opens up, revealing the entire raw data with the request and response objects.

This detailed log can be invaluable when troubleshooting issues or understanding specific interactions. It provides full transparency into each request and response, enabling you to see exactly what data was sent and received.


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=831f1cb98919f6a6d9e2a467db031653" data-og-width="800" width="800" data-og-height="492" height="492" data-path="images/product/product-2.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=177f0f27e7b847950e62a6bc6b0b4786 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=4e952e9099bfc64c971d3cafaa8ef01d 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=5b2d7c6d355ba6d311cae84387bf59ae 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=769de7954401d81d0088c41ffebc4ba1 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=68acb88afdbc7851d0d86a823c69b1b2 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-2.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=84e20bf287a28b6ff392bb0473c734aa 2500w" />


## Share Logs with Teammates

Each log on Portkey has a unique URL. You can copy the link from the address bar and directly share it with anyone in your org.

## Request Status Guide

The Status column on the Logs page gives you a snapshot of the gateway activity for every request.

Portkey’s gateway features—[Cache](/product/ai-gateway/cache-simple-and-semantic), [Retries](/product/ai-gateway/automatic-retries), [Fallback](/product/ai-gateway/fallbacks), [Loadbalance](/product/ai-gateway/load-balancing) are tracked here with their exact states (`disabled`, `triggered`, etc.), making it a breeze to monitor and optimize your usage.

**Common Queries Answered:**

* **Is the cache working?**: Enabled caching but unsure if it's active? The Status column will confirm it for you.
* **How many retries happened?**: Curious about the retry count for a successful request? See it in a glance.
* **Fallback and Loadbalance**: Want to know if load balance is active or which fallback option was triggered? See it in a glance.


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=47bb08ef14ca9168f30d9d8bd8a6aece" data-og-width="800" width="800" data-og-height="419" height="419" data-path="images/product/product-3.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=a0e061d80ce63126ba4e4acc1080a4f5 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=fa5b4b74ad07b845471358f25c855cc8 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=c7336a84ab2c7e4775d4115a784a5fb4 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=0f05d04683f1276b5651159b8176ae27 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=51909df0d9b9fbb24a8a6110aa6f702b 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-3.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=c7f450113466f5a9793942b3798ad393 2500w" />


| Option          | 🔴 Inactive State     | 🟢 Possible Active States                               |
| --------------- | --------------------- | ------------------------------------------------------- |
| **Cache**       | Cache Disabled        | Cache Miss,Cache Refreshed,Cache Hit,Cache Semantic Hit |
| **Retry**       | Retry Not Triggered   | Retry Success on {x} Tries,Retry Failed                 |
| **Fallback**    | Fallback Disabled     | Fallback Active                                         |
| **Loadbalance** | Loadbalancer Disabled | Loadbalancer Active                                     |

## Manual Feedback

As you're viewing logs, you can also add manual feedback on the logs to be analysed and filtered later. This data can be viewed on the [feedback analytics dashboards](/product/observability/analytics#feedback).


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=3aac211557b5a7cea6dc9be7969b2560" data-og-width="800" width="800" data-og-height="522" height="522" data-path="images/product/product-7-1.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=20fa3f54f9e1e2e625de36f0cc0cd577 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=91015866de74ab95e3bd95f519900a29 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=1818f787b7b9ff394a9e500fe1d43443 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=6ab7160e508dfd739fc6e7c149f24ec2 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=c90557ef23489b4d95f5e1f2e19e3933 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-7-1.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=ea2ffeaa64debd951e416a209f97edf8 2500w" />


## Configs & Prompt IDs in Logs

If your request has an attached [Config](/product/ai-gateway/configs) or if it's originating from a [prompt template](/product/prompt-library), you can see the relevant Config or Prompt IDs separately in the log's details on Portkey. And to dig deeper, you can just click on the IDs and Portkey will take you to the respective Config or Prompt playground where you can view the full details.


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=e1884ad3ed0aff3c2484a9a9c6edd2bf" data-og-width="540" width="540" data-og-height="410" height="410" data-path="images/product/product-8-1.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=32817a306d8dedee4c49f33543d03225 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=57c123c4993d87c1c5198836592b839a 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=681d6f5f90ddc8b74073dc72fe3c135a 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=db1006f355401c481e7a39c6c1c59f05 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=b7564ef5795231c46bbee3a3cecebd13 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-8-1.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=9863f600286fa0046b669f46e3f49fef 2500w" />


## Debug Requests with Log Replay

You can rerun any buggy request with just one click, straight from the log details page. The `Replay` button opens your request in a fresh prompt playground where you can rerun the request and edit it right there until it works.


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=59dce817f829583e49a6f0fa273f19a0" data-og-width="650" width="650" data-og-height="370" height="370" data-path="images/product/product-9-1.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=3cc90f4d4bc06b60dfad2acaea4d3855 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=a7ae83eed96d5ddbac89722948ffe597 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=f672b8476f903ff93114bda9b6d8ef55 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=ea1eaf5dcd19232ed28caba7cd7adfd6 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=def1ad4bbfe902086f916048fc56e971 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-9-1.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=7cc61557941d55f97886e903c1e91e9c 2500w" />


<Info>
  `Replay` **button will be inactive for a log in the following cases:**

  1. If the request is sent to any endpoint other than `/chat/completions,` `/completions`, `/embeddings`
  2. If the provider used in the log is archived on Portkey
  3. If the request originates from a prompt template which is called from inside a Config target
</Info>

## DO NOT TRACK

The `DO NOT TRACK` option allows you to process requests without logging the request and response data. When enabled, only high-level statistics like **tokens** used, **cost**, and **latency** will be recorded, while the actual request and response content will be omitted from the logs.

This feature is particularly useful when dealing with sensitive data or complying with data privacy regulations. It ensures that you can still capture critical operational metrics without storing potentially sensitive information in your logs.

To enable `DO NOT TRACK` for a specific request, set the `debug` flag to `false` when instantiating your **Portkey** or **OpenAI** client, or include the `x-portkey-debug:false` header with your request.




    ```Python  theme={"system"}
    from portkey_ai import Portkey

    portkey = Portkey(
        api_key="PORTKEY_API_KEY",
        provider="@OPENAI_PROVIDER",
        debug=False
    )

    response = portkey.chat.completions.create(
        messages=[{'role': 'user', 'content': 'Say this is a test'}],
        model='gpt-4'
    )

    print(response.choices[0].message.content)
    ```


### Side-by-side comparison on how a `debug:false` request will be logged


  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=6cbd23cc741530ff9d0c357e3a3b0131" data-og-width="800" width="800" data-og-height="607" height="607" data-path="images/product/product-10-1.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=57b3c21b545e4055dbd16249b3ade475 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=ab28a4fabbbd97439fe98d2aac80b443 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=fdead86bf96a7033b891940e34a3efa7 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=4c34a6b012e0148420987dea23d10494 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=578ca9cc81d8b17e802fa45808a46429 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/product-10-1.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=931be0d59312b742eb0e9a42e7469510 2500w" />



# Analytics

<Info>
  This feature is available for all plans:-

  * [Developer](https://app.portkey.ai/): 30 days retention
  * [Production](https://app.portkey.ai/): 365 days retention
  * [Enterprise](https://portkey.ai/docs/product/enterprise-offering): Unlimited
</Info>

As soon as you integrate Portkey, you can start to view detailed & real-time analytics on cost, latency and accuracy across all your LLM requests.

The analytics dashboard provides an interactive interface to understand your LLM application Here, you can see various graphs and metrics related to requests to different LLMs, costs, latencies, tokens, user activity, feedback, cache hits, errors, and much more.

The metrics in the Analytics section can help you understand the overall efficiency of your application, discover patterns, identify areas of optimization, and much more.

<Frame>
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=6c880d5ae17f22884436ad3c7b3347d9" data-og-width="600" width="600" data-og-height="348" height="348" data-path="images/product/dashboard.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=9d6c392aaf1649e010ed8cc4b11d3dde 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=d456a9103b9fb5f589766d436f19ff3c 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=abdfe42b663a6615d8237668b1cea902 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=791cd7a60fde6493fc3dd45c9ed3dea3 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=37e405fc70c09b4f36488c542d7ae4ab 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/dashboard.png?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=be50a68424a1f981b971ab05034f52a4 2500w" />
</Frame>

## Charts

The dashboard provides insights into your [users](/product/observability/analytics#users), [errors](/product/observability/analytics#errors), [cache](/product/observability/analytics#cache), [feedback](/product/observability/analytics#feedback) and also summarizes information by [metadata](/product/observability/analytics#metadata-summary).

### Overview

The overview tab is a 70,000ft view of your application's performance. This highlights the cost, tokens used, mean latency, requests and information on your users and top models.

This is a good starting point to then dive deeper.

### Users

The users tab provides an overview of the user information associated with your Portkey requests. This data is derived from the `user` parameter in OpenAI SDK requests or the special `_user` key in the Portkey [metadata header](/product/observability/metadata).

Portkey currently does not provide analytics on usage patterns for individual team members in your Portkey organization. The users tab is designed to track end-user behavior in your application, not internal team usage.

<Frame>
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=7051cea70cb364e1638d3299e9e5aca6" data-og-width="1536" width="1536" data-og-height="804" height="804" data-path="images/product/errors-analytics.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=d4bce9e16af08464772828304e41a88e 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=c2a11762b370049ea2b800d4eff6b11c 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=fe27f9b27add3feb10ee741314560fc4 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=c0ad302906c397cfe1dbcd73418f65d1 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=c4d1b20347605170e97e4de1b5a182ce 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/errors-analytics.avif?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=e14981c9479ae70307fde26ec80378aa 2500w" />
</Frame>

### Errors

Portkey captures errors automatically for API and Accuracy errors. The charts give you a quick sense of error rates allowing you to debug further when needed.

The dashboard also shows you the number of requests rescued by Portkey through the various AI gateway strategies.

<Frame caption="Error Analytics Dashboard">
  <img src="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=a4fdb23a6887dd546711d66c4edb6da9" data-og-width="1536" width="1536" data-og-height="766" height="766" data-path="images/product/users-analytics.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=280&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=6353b498d42b0d85b73382d4328e7aeb 280w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=560&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=c6ec1f4129b730ad09b6a45cf61ab640 560w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=840&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=9f2dbc97f3d120744072a70d1d9503ae 840w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=1100&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=dda167c5e977b87f53321e3ffe77728e 1100w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=1650&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=7f37efce1e8d6b5bd9d779358b8b6f50 1650w, https://mintcdn.com/portkey-docs/_Cb_bj7tVjxcfwsu/images/product/users-analytics.avif?w=2500&fit=max&auto=format&n=_Cb_bj7tVjxcfwsu&q=85&s=ae16fa8bf218de22dcf9938e51edf196 2500w" />
</Frame>

### Cache

When you enable cache through the AI gateway, you can view data on the latency improvements and cost savings due to cache.

### Feedback

Portkey allows you to collect feedback on LLM requests through the logs dashboard or via API. You can view analytics on this feedback collected on this dashboard.

### Metadata Summary

Group your request data by metadata parameters to unlock insights on usage. Select the metadata property to use in the dropdown and view the request data grouped by values of that metadata parameter.

This lets you answer questions like:

1. Which users are we spending the most on?
2. Which organisations have the highest latency?

<Frame caption="Metadata Analytics">
  <img src="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=2da95f164615b237970e7868cd50c709" data-og-width="800" width="800" data-og-height="195" height="195" data-path="images/product/metadata-analytics.avif" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=280&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=0085873397cc7c82c41f64b7c05e2bb9 280w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=560&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=47b3b32d3fa2d7e89bdf107d005a62d7 560w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=840&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=1d1d95c2b5baf66f1de72052c772b4a1 840w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=1100&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=52a27d04a9e625d56214c4ac771c66bf 1100w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=1650&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=e99959bc4b3111df5a9fb0097105e80a 1650w, https://mintcdn.com/portkey-docs/Buc1Vm2P31GSPm3S/images/product/metadata-analytics.avif?w=2500&fit=max&auto=format&n=Buc1Vm2P31GSPm3S&q=85&s=f0e7f531d49cf0ab73668658733e4e5a 2500w" />
</Frame>
