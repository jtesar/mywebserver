IMAGE_NAME = mywebserver

.PHONY: build
build:
	podman build -t $(IMAGE_NAME) .

.PHONY: test
test: build
	podman login -u developer -p $(oc whoami -t) default-route-openshift-image-registry.apps.ocp4.example.com
	podman push $(IMAGE_NAME) default-route-openshift-image-registry.apps.ocp4.example.com/test/$(IMAGE_NAME)
	oc delete all --all
	oc new-app https://github.com/jtesar/mywebserver.git --context-dir=src 
