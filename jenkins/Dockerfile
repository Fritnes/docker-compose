FROM jenkins/jenkins:lts
USER root
RUN apt-get update && apt-get install -y --no-install-recommends gnupg \
	&& install -m 0755 -d /etc/apt/keyrings \
	&& curl -fsSL https://apt.releases.hashicorp.com/gpg -o /tmp/hashicorp.asc \
	&& gpg --dearmor -o /etc/apt/keyrings/hashicorp.gpg /tmp/hashicorp.asc \
	&& chmod a+r /etc/apt/keyrings/hashicorp.gpg \
	&& rm /tmp/hashicorp.asc \
	&& suite="$(. /etc/os-release && printf '%s' "${UBUNTU_CODENAME:-$VERSION_CODENAME}")" \
	&& printf '%s\n' 'Types: deb' 'URIs: https://apt.releases.hashicorp.com' "Suites: $suite" 'Components: main' "Architectures: $(dpkg --print-architecture)" 'Signed-By: /etc/apt/keyrings/hashicorp.gpg' > /etc/apt/sources.list.d/hashicorp.sources
RUN apt-get update && apt-get install -y postgresql-client ansible wget zip terraform
