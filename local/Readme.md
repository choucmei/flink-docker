# build flink-*.tar.gz
cd ${flink-root}
mvn install -DskipTests
tar -cvf flink-*.tar.gz

# download gosu
https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64
https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64.asc

# build docker image
docker build ./ -t tmaster:5000/flink:1.18-SNAPSHO
# push private repo
docker push tmaster:5000/flink:1.18-SNAPSHOT

# example
add flink-conf.yaml
kubernetes.container.image.ref: tmaster:5000/flink:1.18-SNAPSHOT
./bin/kubernetes-session.sh