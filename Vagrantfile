Vagrant.configure('2') do |config|

  config.vm.provider :virtualbox do |vbox, override|
    override.vm.box = 'ubuntu/trusty64'
  end

  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provision :shell, :inline => <<-SH
    apt-get update -q
    apt-get install -qy libmagickwand-dev
    apt-get install -qy git
    cd /tmp
    wget -q https://godeb.s3.amazonaws.com/godeb-amd64.tar.gz
    tar xzvf godeb-amd64.tar.gz && rm godeb-amd64.tar.gz
    mv godeb /usr/bin/godeb
    /usr/bin/godeb install
    echo 'export GOPATH=/go' >> /home/vagrant/.bashrc
    GOPATH=/go go get github.com/gographics/imagick/imagick
  SH

  config.vm.synced_folder ENV["GOPATH"], "/go"
end
