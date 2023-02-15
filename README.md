Hi Reader!

Hope you are doing awesome!

Here are some insights on this Helm Chart:

This is for a web application assuming that application generates some dynamic data and needs a bearer token to authenticate with a secure endpoint. 

Files list and explanation:

Chart.yaml:

Contains the version and name of chart.

values.yaml:

Contains the values that are being utlitized by the template files to deploy the manifests.

values-template:

This contains the values file for different envs i.e. staging, prod, dev, if someone wants to deploy this chart to dev env he can copy the dev values file located in this folder to ../values.yaml file

templates:

This folder contains all the manifest files for the helm chart. 

PROBLEM:

We needed to enable this helm to handle different envs
We needed to handle a bearer token that is to be utlized by our web app to connect to secure endpoints

SOLUTION:

We have made values-template folder that contains values for seperate envs. we can just copy the relevant values file in the chart root directory
We have used the kubernetes secret to create a secret and used kubernetes volume to inject that secret into container path. App can pick up the bearer token from that particular path and use to connect to secure endpoint.

NOTE: There are multiple ways to do this i.e. we can configure a kubernetes secret and inject it inside container and web app code can get that bearer token from the file injected inside container( done in this case ) OR we can inject secret as ENV VARIABLE of app  and app can use ENV variable to hit the secure end point.

TO CHECK LINTING: use "helm lint" command to lint this chart
