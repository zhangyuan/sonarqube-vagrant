Vagrant.configure("2") do |config|
  config.vm.box = "debian/jessie64"
  config.vm.hostname = "sonarqube.box"
  config.vm.provision "docker" do |d|
    d.run "sonarqube",
      args: "--name sonarqube -p 9000:9000 -p 9092:9092"
  end
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "forwarded_port", guest: 9092, host: 9092
end
