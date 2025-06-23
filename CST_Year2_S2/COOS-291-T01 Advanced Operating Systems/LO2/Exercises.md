## Q1
Create a directory off of the `/home` directory called `year2`
Create a new group called `year2`
Create 3 users - `able`, `baker`, `charlie`
- their home directory should be `/home/year2/accountname` (Ex. `/home/year2/charlie`)
- The primary group for each user should be `year2`

```bash
sudo mkdir year2
sudo addgroup year2
sudo adduser --ingroup year2 --home /home/year2/able able
sudo adduser --ingroup year2 --home /home/year2/baker baker
sudo adduser --ingroup year2 --home /home/year2/charlie charlie
```

## Q2
```bash
sudo mkdir /home/trek
sudo addgroup trek
sudo adduser --ingroup trek --home /home/trek/spock spock
sudo adduser --ingroup trek --home /home/trek/scotty scotty
sudo adduser --ingroup trek --home /home/trek/kirk kirk
sudo usermod -aG kirk year2
sudo usermod -aG scotty year2
sudo usermod -aG spock year2
```
