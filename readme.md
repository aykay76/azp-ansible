The purpose of this project is to create a docker image that contains the Microsoft Azure Pipelines agent and Ansible, so that I can run pipelines to trigger Ansible on a private network. In my example this is a home network where I don't want to put computers into the DMZ; it could equally be for computers in private cloud or isolated networks in public cloud.

I would prefer to use Arch but the Azure DevOps agent image is based on Ubuntu, so i'll use that.

So I think i'll start here:
https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux

And finally this:
https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu

I'm hoping this is enough to get what I need. Let's find out!!

Build the container:
`docker build -t azp-ansible .`

Run the container using predefined environment variables:
`docker run -e AZP_URL=$env:AZP_URL -e AZP_TOKEN=$env:AZP_TOKEN -e AZP_AGENT_NAME=$env:AZP_AGENT_NAME azp-ansible:latest`

When creating a pipeline in YAML to use this agent, simply take a starter pipeline and replace the pool:

`pool: 'default'`

where `default` is the name of the pool (unless you changed it).

It's as simple as that!!