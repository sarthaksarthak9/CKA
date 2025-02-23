## Volumes

#### Imagine you have two spaces:

- A folder on your computer (called "/data")
- A folder inside a container (called "/opt")

#### What's happening is:

You're connecting these two folders together
When something saves a file in the container's "/opt" folder, it actually gets saved in your computer's "/data" folder
It's like creating a magic tunnel between these two folders

#### So in this case:

The container generates a random number and saves it to its "/opt" folder
Because of the connection (or "volume mount"), this file actually ends up in your computer's "/data" folder
Even if you delete the container, the file stays safe on your computer because it was really stored there all along



```
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-example
spec:
  volumes:
    - name: data-volume
      hostPath:
        path: /data  # Directory on the host
  containers:
    - name: random-writer
      image: busybox
      command: [ "sh", "-c", "echo $RANDOM > /opt/random.txt && sleep 3600" ]
      volumeMounts:
        - mountPath: /opt  # Path inside the container
          name: data-volume
```

## PV and PVC

- AccessMode of a Persistent Volume (PV) and its corresponding Persistent Volume Claim (PVC) must match for the PVC to successfully bind to the PV.