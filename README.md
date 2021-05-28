# Build
mvn clean package && docker build -t com.ffit.swf/payaralogger .

# RUN

docker rm -f payaralogger || true && docker run -d -p 8080:8080 -p 4848:4848 --name payaralogger com.ffit.swf/payaralogger 