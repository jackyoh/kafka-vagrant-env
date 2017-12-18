require 'yaml'
require 'fileutils'

def read_yaml_file(filename)
  filePath = File.join(File.dirname(__FILE__), filename)
  if !File.file?(filePath)
    puts "\e[31mCannot find file: #{ filePath }\e[0m"
    Kernel.exit(0)
  end
return YAML.load_file(filePath)
end

$node = read_yaml_file("node.yml")

Vagrant.configure("2") do |config|
  config.vm.box = $node["box"]
  config.vm.hostname = $node["hostname"]
  config.ssh.username = $node["username"]
  config.ssh.password = $node["password"]

  if ($node["network"]["bridge"])
    config.vm.network $node["network"]["identifier"], \
                      ip: $node["network"]["ip"], \
                      netmask: $node["network"]["netmask"], \
                      bridge: $node["network"]["bridge"]
  else
    config.vm.network $node["network"]["identifier"], \
                      ip: $node["network"]["ip"], \
                      netmask: $node["network"]["netmask"]
  end

  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.cpus = $node["cpus"]
     vb.memory = $node["memory"]
     vb.name = $node["hostname"]
  end

  # Download and Install zookeeper
  config.vm.provision "shell", name: "Download Zookeeper", \
              inline: "wget http://file-server/sharefolder/common/zookeeper/zookeeper-3.4.6.tar.gz -P /opt"

  config.vm.provision "shell", name: "Decompress zookeeper-3.4.6.tar.gz", \
              inline: "cd /opt && tar zxvf zookeeper-3.4.6.tar.gz"

  config.vm.provision "shell", name: "Copy zoo.cfg.template file", \
              inline: "cp /opt/zookeeper-3.4.6/conf/zoo_sample.cfg /opt/zookeeper-3.4.6/conf/zoo.cfg"

  # Download and Install Kafka
  config.vm.provision "shell", name: "Download Kafka", \
              inline: "wget http://file-server/sharefolder/common/kafka/confluent-oss-4.0.0-2.11.tar.gz -P /opt"

  config.vm.provision "shell", name: "Decompress confluent-oss-4.0.0-2.11.tar.gz", \
              inline: "cd /opt && tar zxvf confluent-oss-4.0.0-2.11.tar.gz"

end

