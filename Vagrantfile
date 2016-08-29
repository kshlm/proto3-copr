SCRIPT= %{
  sudo dnf install tito vim git -y
}
Vagrant.configure("2") do |config|
  config.vm.synced_folder ".", "/vagrant",disabled:true 

  config.vm.define "tito" do |fed|
    fed.vm.hostname = "tito"
    fed.vm.provider "docker" do |d|
      d.image = "kshlm/vagrant-fedora:latest"
      d.has_ssh = true
      d.remains_running = true
      d.name = "tito"
      d.volumes = [ENV["PWD"]+":/home/vagrant/protobuf",
                   ENV["HOME"]+"/.gitconfig:/home/vagrant/.gitconfig",
                   ENV["HOME"]+"/.ssh/id_ed25519:/home/vagrant/.ssh/id_ed25519",
                   "/sys/fs/cgroup:/sys/fs/cgroup:ro"]
      d.create_args = ['--cap-add', 'SYS_ADMIN']
    end
    fed.vm.provision "shell", inline: SCRIPT
  end
end
