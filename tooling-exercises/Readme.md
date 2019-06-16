# Readme

## Tooling overview

https://github.com/tdhd/interpretability-class/blob/master/tooling-exercises/interpretability%20tooling.ipynb

## WIT

### Install docker

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker

sudo usermod -aG docker ${USER}
```

## WIT tool from hosted on EC2

[Interactive WIT](https://github.com/tensorflow/tensorboard/tree/master/tensorboard/plugins/interactive_inference)

[TF WIT](https://www.tensorflow.org/tensorboard/r2/what_if_tool)

[Pair Code WIT](https://pair-code.github.io/what-if-tool)

```bash
# on EC2 instance
wget https://storage.googleapis.com/what-if-tool-resources/uci-census-demo/uci-census-demo.zip
unzip uci-census-demo.zip
export MODEL_PATH=/path/to/uci_census/model
# run this in the background or dedicated screen
# (screen -S docker, and then execute below command)
docker run -p 8500:8500 --mount type=bind,source=${MODEL_PATH},target=/models/uci_income -e MODEL_NAME=uci_income -t tensorflow/serving
# run tensorboard on the EC2 instance
tensorboard --logdir /tmp/wit-logs/
```

After this, you can connect to the public IP address of the EC2 instance, which is usually `http://<ec-public-ip>:6006`. In case you cannot connect to the this address, you might have to edit the EC2 security group to allow connects from your IP, or anywhere else to the tensorboard port (6006 in this case).

If you don't have access to the security group configuration you can use SSH-based port forwarding like

```bash
ssh -i ~/.ssh/dsr -L 8080:localhost:6006 ubuntu@<ec2-public-ip> -N
```

where this allows you to connect to `http://localhost:8080` which will be forwarded to the tensorboard UI on EC2 at port `6006`.

Then, choose WIT from Tensorboard and add docker-hosted tensorflow serving like

![setup](https://github.com/tdhd/interpretability-class/blob/master/tooling-exercises/what_if_tool_demo_setup.png)
