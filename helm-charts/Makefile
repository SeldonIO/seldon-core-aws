CHARTS=seldon-core-aws


build_all:
	make clean package get_index update_index

push_all:
	gsutil cp build/index.yaml build/*.tgz gs://seldon-aws-charts/


package:
	mkdir -p build && \
		helm package $(CHARTS) && \
		mv *.tgz build/

get_index:
	mkdir -p build && \
		wget https://storage.googleapis.com/seldon-aws-charts/index.yaml && \
		mv index.yaml build/ && \
		cp -v ./build/index.yaml ./build/index.yaml.orig

update_index:
	cd build && \
		helm repo index --merge index.yaml --url https://storage.googleapis.com/seldon-aws-charts ./

clean:
	rm -rfv build

