## Hyper-V Manger Setup

Open Hyper-V Manager

1. Quick Create...
2. Ubuntu 22.04 LTS
3. Create Virtual Machine
### If not installed

Run:

```
appwiz.cpl
```
Turn Windows Features on of off -> Enable Windows Hyper-V

Restart PC.
### Virtual Network

New Virtual Switch -> External

Ensure this is check mark is checked (Will lose connectivity).

![[Pasted image 20250108100500.png]]

Select your VM, Settings, Network Adapter -> Choose the new External Switch.
Connect to VM.
## Setting up Ubuntu

Enter languages and time.
### Who are you

Name: Brody
Computer: coos291b-brody
Username: student
password: admin
### Xorg login

Sign in with username: student, password: admin (we created this).
If this does not work, click View on the VM window and disable "Enhanced session".
### First time login

You do not have to create an account for Ubuntu.