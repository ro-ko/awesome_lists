# note for monitoring utilization of independent GPU nodes

When there are many independent machines in your group, for example, my group has 9 single machines with a total of 30 cards (RTX 3090/4090). I want to know the GPU utilization of these machines over a period of time (generally commercial clusters will have Such functions), you can use the open-source tools mentioned below.

1. Use jupyterlab_nvdashboard

`https://github.com/rapidsai/jupyterlab-nvdashboard`

Run this on the node you want to monitor
```
python -m jupyterlab_nvdashboard.server 9988
```

Then you can open a html to see the log `http://10.30.8.195:9988/GPU-Resources`
The log is only saved on the web page. No database is used. So you need to keep the web page open.


2. use rntop from run-ai

`https://github.com/run-ai/rntop`

This is better for monitoring multiple nodes. 
Principle：pass `ssh user@IP nvidia-smi` each node then logs GPU utilization to a file.

Suppose you have a head node. Need to put the head node's id_rsa.pub to all the GPU nodes' authorized_keys.

Run the following in a screen. The output file will be saved to `/home/junweil/nv_monitoring/rntop.log`
```
(base) junweil@junwei-home-lab:~/nv_monitoring$ sudo docker run -it --rm -v $HOME/.ssh:/root/.ssh -v $HOME/nv_monitoring:/host runai/rntop --output /host/rntop.log junweil@machine-1-IP junweil@machine-2-IP ...
```

Then you can upload the log file to `https://run-ai.github.io/rntop-board/` and see the utilization over time.
