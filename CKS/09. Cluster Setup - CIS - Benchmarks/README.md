CIS - Center for Internet Security
- best pratices for the security contiguration of a target system.
- covering more than 14 technology groups.
- developed through a unique consensus-based process comprised of cybersecurity professionals and subject matter experts arount the world.


# how to run
https://github.com/aquasecurity/kube-bench/blob/main/docs/running.md


# run on master
docker run --pid=host -v /etc:/etc:ro -v /var:/var:ro -t aquasec/kube-bench:latest run --targets=master --version 1.22

# run on worker
docker run --pid=host -v /etc:/etc:ro -v /var:/var:ro -t aquasec/kube-bench:latest run --targets=node --version 1.22
