### terraform-example-cloud-sql
```
wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy
chmod +x cloud_sql_proxy
export GOOGLE_PROJECT=$(gcloud config get-value project)
MYSQL_DB_NAME=$(terraform output -json | jq -r '.instance_name.value')
MYSQL_CONN_NAME="${GOOGLE_PROJECT}:us-central1:${MYSQL_DB_NAME}"
./cloud_sql_proxy -instances=${MYSQL_CONN_NAME}=tcp:3306
```
### another session
```
echo MYSQL_PASSWORD=$(terraform output -json | jq -r '.generated_user_password.value')
mysql -udefault -p --host 127.0.0.1 default
```
