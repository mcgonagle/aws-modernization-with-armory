---
title: "7. Armory OPA Lab"
chapter: true
weight: 10
---

## 1. Delete Spinnaker
    kubectl delete ns spinnaker


## 2. Create NameSpace Spinnaker
    kubectl create ns spinnaker


## 3. Download kubectl command 
    curl -LO https://dl.k8s.io/release/v1.19.0/bin/linux/amd64/kubectl
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

## 4. Chmod +x kubectl command
    chmod +x kubectl


## 5. Create secrets
    cd spinnaker-kustomize-patches/secrets; ./create-secrets.sh



## 6. Edit kustomization.yml
    configMapGenerator:
      # ConfigMap holding OPA policy definitions to use by Armory's policy engine. Required by patch-policyengine.yml
      - name: spin-policies
        files:
          - armory/policies/manual-judgement.rego


## 7. Edit the spin-polcies config map
	remove the 1 := 0, it is a rego null value

## 8. Run kustomize
    ~/kubectl apply -k /home/ec2-user/spinnaker-kustomize-patches


## 9. Watch for Pods to Come Up
    watch kubectl get pods -n spinnaker


## 10. Get Spin Deck URL
    kubectl get svc spin-deck -n spinnaker 

----------
## 1. Create an application in your spinnaker installation.

## 2. Create a pipeline in your application.

## 3. Try to save a pipeline without a manual judgment

## 4. Notice that the pipeline can not be saved due to the Open Policy Agent preventing it.

----------
## OPA

OPA Rules/Policies


    kubectl -n spinnaker create configmap manual-judgment --from-file=manual-judgment.rego


    kubectl -n spinnaker label configmap manual-judgment openpolicyagent.org/policy=rego


## Go over policy engine Example Policies

https://docs.armory.io/docs/armory-admin/policy-engine/policy-engine-use/example-policies/


