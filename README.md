# Start-GPT Package

![Run of the Start-GPT Package](/run.gif)

"It's like StartGPT got a `brew install`", made possible by [Kurtosis](https://www.kurtosis.com/).

**NOTE**: This now runs with 0.4.0 that drops support for Milvus, Weaviate and PineCone. You can run Kurtosis against 0.3.1 by doing `kurtosis run github.com/khulnasoft-lab/startgpt-package@0.3.1` with the desired arguments

## Run StartGPT in the browser (no installation needed)

1. If you don't have an OpenAI API key, get one [here](https://platform.openai.com/account/api-keys)
1. Click [this link](https://gitpod.io/?editor=code#https://github.com/khulnasoft-lab/startgpt-package) to open a Gitpod, selecting "Continue" to use the default resources
1. Wait for the Gitpod to boot up and the terminal to finish installing Kurtosis (should take ~30 seconds)
1. Run the following in the terminal (replacing `YOUR_API_KEY_HERE` with your OpenAI API key)
   ```bash
   kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE"}'
   ```
1. When installing & starting StartGPT has finished, run the following in the terminal to open the StartGPT prompt:
   ```bash
   kurtosis service shell startgpt startgpt --exec "python -m startgpt"
   ```
1. Use StartGPT as you please!

![Run of the Start-GPT Package](/gitpod.png)

## Run StartGPT on your machine

1. If you don't have an OpenAI API key, get one [here](https://platform.openai.com/account/api-keys)
1. Install Kurtosis using [these instructions](https://docs.kurtosis.com/install)
1. Run the following in your terminal (replacing `YOUR_API_KEY_HERE` with your OpenAI API key)
   ```bash
   kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE"}'
   ```
1. When installing & starting StartGPT has finished, run the following in your terminal to open the StartGPT prompt:
   ```bash
   kurtosis service shell startgpt startgpt
   ```
and then within the prompt:
   ```bash
   > python -m startgpt
   ```
1. Use StartGPT as you please! To destroy the StartGPT instance, run:
   ```
   kurtosis enclave rm -f startgpt
   ```

## Configuring StartGPT (including memory backend)

To pass any of the StartGPT configuration values listed [here](https://github.com/KhulnaSoft/Start-GPT/blob/master/.env.template), pass the argument as a property of the JSON object you're passing to Kurtosis just like you passed in `OPENAI_API_KEY`.

For example, this is how you'd pass the `RESTRICT_TO_WORKSPACE` flag:

```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE", "RESTRICT_TO_WORKSPACE": "False"}'
```

**NOTE:** this package spins up StartGPT using the `local` backend by default. Other backends are available by setting the `MEMORY_BACKEND` parameter in the JSON object you pass in when you run the `kurtosis run` command above. 

For example, to set the `redis` memory backend:

```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE", "MEMORY_BACKEND": "redis"}'
```

**NOTE**: Redis isn't working with 0.4.0 for now

To run with a different image other than the one hardcoded in `main.star` use
```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE", "STARTGPT_IMAGE": "significantgravitas/auto-gpt:v0.4.0"}'
```

## Using StartGPT plugins

Kurtosis supports the `ALLOWLISTED_PLUGINS` configuration flag that StartGPT ships with. For example, to run the `StartGPTTwitter` plugin do the following:

```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE", "ALLOWLISTED_PLUGINS": "StartGPTTwitter"}'
```

To get multiple plugins running at the same time; separate them with comma without spaces like so:

```
kurtosis run github.com/khulnasoft-lab/startgpt-package --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE", "ALLOWLISTED_PLUGINS": "StartGPTTwitter,StartGPTEmailPlugin"}'
```

Under the hood, Kurtosis will download and install the package for you. 

As of now the following plugins are supported:

### First Party
- [StartGPTTwitter](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTEmailPlugin](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTSceneXPlugin](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTBingSearch](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTNewsSearch](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTWikipediaSearch](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTApiTools](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTRandomValues](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTSpacePlugin](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTBaiduSearch](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTBluesky](https://github.com/KhulnaSoft/Start-GPT-Plugins)
- [StartGPTAlpacaTraderPlugin](https://github.com/danikhan632/Start-GPT-AlpacaTrader-Plugin)
- [StartGPTUserInput](https://github.com/HFrovinJensen/Start-GPT-User-Input-Plugin)
- [BingAI](https://github.com/gravelBridge/StartGPT-BingAI)
- [StartGPTCryptoPlugin](https://github.com/isaiahbjork/Start-GPT-Crypto-Plugin)
- [StartGPTDiscord](https://github.com/gravelBridge/StartGPT-Discord)
- [StartGPTDollyPlugin](https://github.com/pr-0f3t/Start-GPT-Dolly-Plugin)

### Third Party
- [StartGPTGoogleAnalyticsPlugin](https://github.com/isaiahbjork/Start-GPT-Google-Analytics-Plugin)
- [StartGPT_IFTTT](https://github.com/AntonioCiolino/StartGPT-IFTTT)
- [StartGPT_Zapier](https://github.com/AntonioCiolino/StartGPT-Zapier)
- [StartGPT_YouTube](https://github.com/jpetzke/StartGPT-YouTube)
- [StartGPTPMPlugin](https://github.com/minfenglu/StartGPT-PM-Plugin)
- [StartGPTWolframAlpha](https://github.com/gravelBridge/StartGPT-WolframAlpha)
- [StartGPTTodoistPlugin](https://github.com/danikhan632/Start-GPT-Todoist-Plugin)
- [StartGPTMessagesPlugin](https://github.com/danikhan632/Start-GPT-Messages-Plugin)
- [StartGPTWebInteraction](https://github.com/gravelBridge/StartGPT-Web-Interaction)
- [StartGPTNotion](https://github.com/doutv/Start-GPT-Notion)
- [SystemInformationPlugin](https://github.com/hdkiller/Start-GPT-SystemInfo)

To add support for more plugins, simply create an issue or create a PR adding an entry to [`plugins.star`](https://github.com/khulnasoft-lab/startgpt-package/blob/main/plugins.star).

## Run without OpenAI

We understand OpenAI can be expensive for some people; more-ever some people might be trying to use this with their own models. StartGPT-Package supports running StartGPT against a `GPT4All` model that runs via `LocalAI`. To use a local model -

```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package '{"GPT_4ALL": true}'
```

This uses the `https://gpt4all.io/models/ggml-gpt4all-j.bin` model default

To use a different model try the `MODEL_URL` parameter like -


```bash
kurtosis run github.com/khulnasoft-lab/startgpt-package '{"GPT_4ALL": true, "MODEL_URL": "https://gpt4all.io/models/ggml-gpt4all-l13b-snoozy.bin"}'
```

## Development

To develop on this package, clone this repo and run the following:

```bash
kurtosis run . --enclave startgpt '{"OPENAI_API_KEY": "YOUR_API_KEY_HERE"}'
```

Note the `.` - this tells Kurtosis to use the version of the package on your local machine (rather than the version on Github).

Kurtosis also has [an extension available on the VSCode marketplace](https://marketplace.visualstudio.com/items?itemName=Kurtosis.kurtosis-extension) that provides syntax highlighting and autocompletion for the Starlark that this package is composed of.

## Feedback or Questions?

Let us know in our [Discord](https://discord.gg/eBWFjGtm) or on [Twitter @KurtosisTech](https://twitter.com/KurtosisTech)!

Feel free to create an issue on GitHub if you have any bugs or feature requests.
