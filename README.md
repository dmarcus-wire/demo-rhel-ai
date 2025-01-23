# Demo RHEL AI

Red Hat Enterprise Linux AI allows you to do the following:

- Host an LLM and interact with the open source Granite family of Large Language Models (LLMs).
- Using the LAB method, create and add your own knowledge or skills data in a Git repository. Then, fine-tune a model on that data with minimal machine learning background.
- Interact with the model that is fine-tuned with your data.

## Setup

demo.redhat.com - RHEL AI (GA) VM
- RHEL AI (GA)
- InstructLab (version reflects RHEL AI release)
- Nvidia L4 (24GB) GPU (g6.xlarge)
- Optional 4 x L4 via dropdown (g6.12xlarge)
- ssh access

## Procedure

Version 1.3 [Release notes](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/release_notes)

### Before you start
- RHEL AI image includes InstructLab, RHEL 9.4, and various inference and training software, including vLLM and DeepSpeed.
- For Red Hat Enterprise Linux AI version 1.3 general availability, your data must be hosted in a Git repository.
- Hosting your knowledge files on your local system is currently not supported on RHEL AI version 1.3.
- Knowledge for an AI model consists of data and facts.
- Skills are the information that trains an AI model on how to do something

### Getting Started

[source](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/getting_started)

```sh
# view your machine’s information
$ ilab system info

# Initialize InstructLab
$ ilab config init

# The RHEL AI CLI starts setting up your environment and config.yaml file

# Review your config file
$ ilab config show

# You can manually edit the file for changes
# $ ilab config edit

# List models (default is empty)
$ ilab model list

# or use 
$ ls ~/.cache/instructlab/models

# Log into Registry.redhat.io
$ podman login registry.redhat.io

# Search for granite models
$ podman search granite

# Download the adaptors
$ ilab model download --repository docker://registry.redhat.io/rhelai1/knowledge-adapter-v3 --release latest

# Download additional models
# $ ilab model download --repository docker://<repository_and_model> --release <release>
$ ilab model download --repository docker://registry.redhat.io/rhelai1/granite-8b-starter-v1 --release latest

# Serve the model
$ ilab model serve

# You can serve a different than default model using
# $ ilab model serve --model-path <model-path>

# You can set up a systemd service so that the ilab model serve command runs as a running service.
[source](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/building_your_rhel_ai_environment/serving_and_chatting#creating_systemd_serving)

# You can serve an inference endpoint and allow others to interact with models provided with Red Hat Enterprise Linux AI on secure connections by creating a systemd service and setting up a nginx reverse proxy that exposes a secure endpoint. 
[source](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/building_your_rhel_ai_environment/serving_and_chatting#creating_secure_endpoint)

# To chat with the default model (By default, the ilab CLI does not use authentication.)
$ ilab model chat
```

### Creating skills and knowledge YAML files

#### Creating knowledge

- [ ] You installed RHEL AI with the bootable container image.
- [ ] You installed the git CLI.
- [ ] You initialized InstructLab and can use the ilab CLI.
- [ ] You have root user access on your machine.

[source](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/creating_skills_and_knowledge_yaml_files)

### Generating a custom LLM using RHEL AI

[source](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.3/html/generating_a_custom_llm_using_rhel_ai)