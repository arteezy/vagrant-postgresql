Vagrant.configure("2") do |config|
  config.vm.box     = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.omnibus.chef_version = :latest

  config.vm.define "database" do |cfg|
    cfg.vm.network "forwarded_port", guest: 5432, host: 5432
    cfg.vm.provision :chef_solo do |chef|
      chef.provisioning_path = "/tmp/vagrant-chef-solo"
      chef.file_cache_path = chef.provisioning_path
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe("apt")
      chef.add_recipe("postgresql::server")
      chef.json = {
        :postgresql => {
          :users => [
            {
              :username => "vagrant",
              :password => "password",
              :superuser => true,
              :createdb => true,
              :login => true
            }
          ],
          :databases => [
            {
              :name => "vagrant",
              :owner => "vagrant",
              :template => "template0",
              :encoding => "utf8",
              :locale => "en_US.UTF8"
            }
          ],
          :pg_hba => [
            {:type => 'host', :db => 'all', :user => 'all', :addr => '0.0.0.0/0', :method => 'md5'},
            {:type => 'host', :db => 'all', :user => 'all', :addr => '::1/0',     :method => 'md5'}
          ],
          :listen_addresses => '*'
        }
      }
    end
  end
end
