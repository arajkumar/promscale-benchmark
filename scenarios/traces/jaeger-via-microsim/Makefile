NS="microsim"

.PHONY: all
all: install

.PHONY: helm-deps
helm-deps:
	helm dependency update chart/


.PHONY: install upgrade deploy
deploy: install
upgrade: install
install: helm-deps
	helm upgrade --install microsim chart \
		--wait \
		--timeout 15m \
		--namespace "$(NS)" \
		--create-namespace \
		-f values.yaml

.PHONY: uninstall
uninstall:
	helm uninstall microsim --namespace "$(NS)"

jaeger-ui:
	kubectl port-forward -n "$(NS)" svc/microsim-jaeger-query 16686:80

otel:
	helm upgrade --install microsimotel chart \
		--wait \
		--timeout 15m \
		--namespace "$(NS)" \
		--create-namespace \
		-f values-otel.yaml
