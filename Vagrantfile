LOCAL_COMPOSE_YAML_PATH = File.join(File.dirname(__FILE__), 'docker-compose.yml')

SONARQUBE_HOME = "/sonarqube"

INATALL_DOCKER_COMPOSE_SCRIPT = <<-SCRIPT
apt-get update && apt-get install -y python-pip libyaml-dev python-dev
pip install docker-compose
SCRIPT

RUN_SONARQUBE_SCRIPT = <<-SCRIPT
cd #{SONARQUBE_HOME} && \
docker-compose up -d
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "debian/jessie64"
  config.vm.hostname = "sonarqube.box"
  config.vm.provision "docker"
  
  config.vm.provision "shell", inline: "mkdir #{SONARQUBE_HOME} && chmod 777 #{SONARQUBE_HOME}"
  config.vm.provision "file", source: LOCAL_COMPOSE_YAML_PATH, destination: "#{SONARQUBE_HOME}/docker-compose.yml"

  config.vm.provision "shell", inline: INATALL_DOCKER_COMPOSE_SCRIPT

  config.vm.provision "shell", inline: RUN_SONARQUBE_SCRIPT, run: "always"

  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "forwarded_port", guest: 9092, host: 9092
end


# 