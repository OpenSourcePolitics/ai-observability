namespace := langfuse
version := 1.2.3

upgrade:
	helm upgrade --install \
		--namespace ${namespace} \
		--create-namespace \
		--values values-prod.yaml \
		langfuse langfuse-k8s/langfuse --version ${version}