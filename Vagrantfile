Vagrant.configure("2") do |config|
  config.vm.guest = :openbsd
  config.ssh.shell = "ksh -l"
  config.ssh.username = "root"
  config.ssh.password = "vagrant"
  config.vm.define "openbsd-presenter" do |cfg|
    cfg.vm.box = "obsd65"
    cfg.vm.hostname = "openbsd-presenter"
    cfg.vm.synced_folder "./provision", "/vagrant", type: "rsync", rsync__exclude: ".git/", rsync__chown: false
  
    diskfile = File.realpath( "." ).to_s + "/home_dir.vdi"
    cfg.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 512]
      #v.gui = true;
      if !File.exist?(diskfile)
        v.customize ["createhd", "--filename", diskfile, "--format", "VDI", "--size", 5120 ]
      end
      v.customize ["storageattach", :id, "--storagectl", "IDE Controller", "--port", 1, "--device", 1, "--type", "hdd", "--medium", diskfile]
    end

    cfg.vm.provision "shell", inline: "pkg_add ansible"
  end

end

