Vagrant.configure('2') do |config|
  config.vm.box = 'obnox/fedora25-64-lxc'
  config.vm.hostname = 'ansible-role-mpd-fedora-25'

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.sudo = true
  end

  config.vm.provision 'shell' do |s|
    s.keep_color = true
    s.inline = <<SCRIPT
systemctl start mpd.service || { echo "could not start mpd" && exit 1; ]
sleep 1
mpc version || { echo "could not get version of mpd" && exit 1; }
systemctl stop mpd.service

cd /vagrant/
ansible-playbook playbook.yml --connection local 2>&1 | tee /tmp/ansible.log

# Remove colors from log file
sed -i -r "s/\\x1B\\[([0-9]{1,2}(;[0-9]{1,2})?)?[m|K]//g" /tmp/ansible.log

# Test for errors
test -n "$(grep -L 'ERROR' /tmp/ansible.log)" \
    && { echo "Errors test: pass"; } \
    || { echo "Errors test: fail" && exit 1; }

# Test for warnings
test -n "$(grep -L 'WARNING' /tmp/ansible.log)" \
    && { echo "Warnings test: pass"; } \
    || { echo "Warnings test: fail" && exit 1; }

# Test for idempotence
grep -q "changed=0.*failed=0" /tmp/ansible.log \
    && { echo "Idempotence test: pass"; } \
    || { echo "Idempotence test: fail" && exit 1; }
SCRIPT
  end
end
