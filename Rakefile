require "rake/testtask"
require "yard"

Rake::TestTask.new do |t|
    t.libs << "lib"
    t.libs << "lib/pandocomatic"
    t.test_files = FileList["test/test_helper.rb", "test/unit/*.rb", "test/spec/*.rb"]
    t.warning = false
    t.verbose = true
end

YARD::Rake::YardocTask.new do |t|
    t.files = ['lib/**/*.rb']
end

task :generate_docs do
    sh %{
    cd documentation;
    ../test/pandocomatic.rb --data-dir data-dir --config config.yaml --input manual2.md --output ../index.md;
    ../test/pandocomatic.rb --data-dir data-dir --config config.yaml --input README.md --output ../README.md
    }
end

task :build do
    Rake::Task['test'].execute
    Rake::Task['yard'].execute
    sh "gem build pandocomatic.gemspec; mv *.gem releases"
    Rake::Task["generate_docs"].execute
end

task :default => :test
