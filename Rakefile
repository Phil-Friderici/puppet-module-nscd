require 'puppetlabs_spec_helper/rake_tasks'
require 'puppet-lint/tasks/puppet-lint'
PuppetLint.configuration.send('disable_80chars')
PuppetLint.configuration.send('disable_140chars')
PuppetLint.configuration.relative = true
PuppetLint.configuration.ignore_paths = ['spec/**/*.pp', 'pkg/**/*.pp', 'vendor/**/*.pp']

desc 'Validate manifests, templates, ruby files and shell scripts'
task :validate do
  Dir['spec/**/*.rb', 'lib/**/*.rb'].each do |ruby_file|
    sh "ruby -c #{ruby_file}" unless ruby_file =~ /spec\/fixtures/
  end
  Dir['files/**/*.sh'].each do |shell_script|
    sh "bash -n #{shell_script}"
  end
end

desc 'Validate that README.md documents all parameters for each class'
task :validate_readme do
  Dir['manifests/**/*.pp'].each do |manifest|
    sh "ext/check_readme.sh #{manifest} README.md"
  end
end
