desc "Update"
task :update do
  src_path = "x-editable-src"
  dist_path = "#{src_path}/dist/bootstrap-editable"
  dist_ext = "#{src_path}/dist/inputs-ext"

  system("rm -rf #{src_path}")

  system("git clone https://github.com/vitalets/x-editable #{src_path}")
  system("cd #{src_path} && npm install")
  system("cd #{src_path} && grunt build")

  system("cp #{dist_path}/img/clear.png vendor/assets/images/")
  system("cp #{dist_path}/img/loading.gif vendor/assets/images/")
  system("cp #{dist_path}/css/bootstrap-editable.css vendor/assets/stylesheets/bootstrap-editable.scss")
  system("cp #{dist_path}/js/bootstrap-editable.js vendor/assets/javascripts/")
  system("cp #{dist_ext}/wysihtml5/wysihtml5.js vendor/assets/javascripts/editable-bootstrap-wysihtml5.js")

  fixes

  system("rm -rf x-editable-src")
end

def fixes
  replace_string_in_file("vendor/assets/stylesheets/bootstrap-editable.scss", "url('../img/loading.gif')", "image-url('loading.gif')")
  replace_string_in_file("vendor/assets/stylesheets/bootstrap-editable.scss", "url('../img/clear.png')", "image-url('clear.png')")
end

def replace_string_in_file(file, find, replace)
  file_content = File.read(file)

  File.open(file, "w") do |f|
    f.puts file_content.gsub!(find, replace)
  end
end

desc "Build"
task "build" do
  system("gem build bootstrap-x-editable-rails.gemspec")
end
