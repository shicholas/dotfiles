require 'rake'
require 'pathname'

desc "install the dot files into user's home directory"
task :install do
  # Install Hombrew
  system %{brew install $(< $PWD/brewlist.txt)}

  Dir['*'].each do |file|
    next if %w[
      brewlist.txt
      bashrc
      Rakefile
      README.md
      .gitignore
      etc-hosts.txt
      vscode.json
    ].include? file

    next if Pathname(file).directory?

    if File.exist?(File.join(ENV['HOME'], ".#{file}"))
      replace_file(file)
    else
      link_file(file)
    end
  end
end

def replace_file(file)
  system %(rm "$HOME/.#{file}")
  link_file(file)
end

def link_file(file)
  puts "linking ~/.#{file}"
  system %(ln -s "$PWD/#{file}" "$HOME/.#{file}")
end
