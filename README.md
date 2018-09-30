# Kubernetes
Setting up a local kubernetes system based on MiniKube and Hyper-V

# Installation

## Usefull links
- https://medium.com/jsonlovesyaml/12-step-tutorial-to-setup-kubernetes-on-your-windows-10-laptop-b7784b2253ce
- https://www.assistanz.com/installing-minikube-on-windows-10-using-hyper-v/
- https://medium.com/@maumribeiro/running-your-own-docker-images-in-minikube-for-windows-ea7383d931f6
- https://rominirani.com/tutorial-getting-started-with-kubernetes-on-your-windows-laptop-with-minikube-3269b54a226


## Install [chocolatey](https://chocolatey.org/)
https://medium.com/@JockDaRock/installing-the-chocolatey-package-manager-for-windows-3b1bdd0dbb49
Open command prompt or WindowsPowerShell as administrator
Run
> @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

## Install MiniKube and kubernetes-cli

I was forced to install an older version and removing the OpenSSH feature in windoes because of the following error:
`Error dialing TCP: ssh: handshake failed: ssh: unable to authenticate, attempted methods [none publickey], no supported methods remain`

> choco install minikube --version 0.27.0

> choco install kubernetes-cli


## Start MiniKube
Make sure there is an Switch called "External", see also https://kubernetes.io/docs/setup/minikube/

> minikube start --vm-driver="hyperv" --hyperv-virtual-switch="External" --memory 4096 --v=7 --alsologtostderr


## Testing
> kubectl get pods -n kube-system

![kubectl](https://user-images.githubusercontent.com/29073072/46258450-416f0480-c4cb-11e8-9b10-3d0e88f41a0e.png)

> minikube dashboard

![dashboard](https://user-images.githubusercontent.com/29073072/46258449-3fa54100-c4cb-11e8-9bc9-75855a608576.png)

### Increasing memory
After everything was successful, tried to increase the amount of memory directly in Hyper-V manager. After that I couldn't get it working again, at least not accessing the cluster via the dashboard. So I deleted the .minikube folder in the users-folder and the VM, then re-installed it again with the `--memory 4096` option.
