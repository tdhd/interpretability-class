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

### Start WIT

https://www.tensorflow.org/tensorboard/r2/what_if_tool
https://pair-code.github.io/what-if-tool/

```bash
# download pretrained from https://storage.googleapis.com/what-if-tool-resources/uci-census-demo/uci-census-demo.zip
wget https://storage.googleapis.com/what-if-tool-resources/uci-census-demo/uci-census-demo.zip
unzip uci-census-demo.zip
export MODEL_PATH=/path/to/uci_census/model
docker run -p 8500:8500 --mount type=bind,source=${MODEL_PATH},target=/models/uci_income -e MODEL_NAME=uci_income -t tensorflow/serving
tensorboard --logdir /tmp/wit-logs/
# open tensorboard in browser and select What-If tool from top-left dropdown
```

