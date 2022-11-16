
show-sa:
	kubectl get sa mj-demo -o yaml

install:
	helm upgrade --install external-secrets \
		external-secrets/external-secrets \
		-n external-secrets \
		--create-namespace \
		--wait

create-aws-secret:
	aws secretsmanager create-secret --name my-password --secret-string "password1234"

update-aws-secret:
	aws secretsmanager update-secret --secret-id my-password --secret-string "$(shell pwgen -s 40 1)"

create-aws-secret-json:
	aws secretsmanager create-secret --name /dev/myapp/db-creds --secret-string '{"username": "admin", "password":"1234"}'

cleanup:
	aws secretsmanager delete-secret --secret-id my-password --force-delete-without-recovery --region eu-central-1
	aws secretsmanager delete-secret --secret-id my-secret-json --force-delete-without-recovery --region eu-central-1
	aws secretsmanager delete-secret --secret-id /dev/myapp/db-creds --force-delete-without-recovery --region eu-central-1
	helm uninstall external-secrets -n external-secrets
	aws secretsmanager list-secrets --region eu-central-1

