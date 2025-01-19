## ConfigMap

A ConfigMap is a Kubernetes resource used to store non-sensitive configuration data as key-value pairs. It allows you to decouple configuration from application code, making applications more portable and easier to manage.


```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  # Key-value pairs
  ENV_VAR_NAME: "value"
  ANOTHER_VAR: "another_value"

  # Configuration file as a key-value pair
  app-config.properties: |
    server.port=8080
    logging.level=INFO
```

## To use cm in Pods
```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-demo-pod
spec:
  containers:
    - name: demo
      image: alpine
      command: ["sleep", "3600"]
      env:
        # Define the environment variable
        - name: PLAYER_INITIAL_LIVES # Notice that the case is different here
                                     # from the key name in the ConfigMap.
          valueFrom:
            configMapKeyRef:
              name: game-demo           # The ConfigMap this value comes from.
              key: player_initial_lives # The key to fetch.
        - name: UI_PROPERTIES_FILE_NAME
          valueFrom:
            configMapKeyRef:
              name: game-demo
              key: ui_properties_file_name       
```