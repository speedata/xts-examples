require "digest"
require "pathname"

# The xts binary to use. The CI installs the latest release into PATH,
# locally XTS=../xts/bin/xts rake qa checks against a development build.
# A path is made absolute, since xts runs in the example's directory.
XTS = ENV["XTS"] ? File.expand_path(ENV["XTS"]) : "xts"
ROOT = Pathname.new(__dir__).freeze

# Every directory with a layout.xml is an example. An optional argument
# limits a task to one example, given as its directory: rake qa[technical/zugferd]
def examples(only = nil)
  return [ROOT.join(only)] if only
  Dir.glob("**/layout.xml", base: ROOT).map { |f| ROOT.join(f).dirname }.sort
end

def rel(dir)
  dir.relative_path_from(ROOT).to_s
end

# Runs xts in the example directory. xts.cfg of the example is read from
# there (pdfa, runs, ...). --suppressinfo drops dates and ids from the
# PDF, so two runs of the same layout with the same xts are byte
# identical and can be compared by hash.
def run_xts(dir, jobname)
  data = dir.join("data.xml").exist? ? [] : ["--dummy"]
  sh XTS, "--suppressinfo", "--quiet", "--jobname", jobname, *data, chdir: dir.to_s
end

def same_as_result?(dir)
  Digest::SHA256.file(dir.join("xts.pdf")) == Digest::SHA256.file(dir.join("result.pdf"))
end

# Any byte difference counts, also an invisible one in the metadata or
# the structure tree. A matching xts.pdf is removed, so the xts.pdf
# files left over are the differing ones (the CI uploads them).
desc "Run every example and compare the PDF with result.pdf by hash"
task :qa, [:only] do |t, args|
  failed = []
  examples(args[:only]).each do |dir|
    run_xts(dir, "xts")
    if same_as_result?(dir)
      rm_f dir.join("xts.pdf"), verbose: false
      puts "ok       #{rel(dir)}"
    else
      failed << rel(dir)
      puts "differs  #{rel(dir)}"
    end
  end
  abort "#{failed.size} example(s) differ from result.pdf: #{failed.join(', ')}. rake compare shows whether the pages differ." unless failed.empty?
end

# Needs ImageMagick and Ghostscript. Tells a visible difference from one
# only in the bytes, for examples whose hash differs.
desc "Compare the pages of every example (or of one) whose PDF differs from result.pdf by hash"
task :compare, [:only] do |t, args|
  failed = []
  examples(args[:only]).each do |dir|
    run_xts(dir, "xts")
    next puts("ok       #{rel(dir)}") if same_as_result?(dir)
    puts "differs  #{rel(dir)}, comparing the pages"
    failed << rel(dir) unless system(XTS, "compare", "--reference", "result", dir.to_s)
  end
  abort "#{failed.size} example(s) look different: #{failed.join(', ')}. See compare-report.html and the pagediff-*.png files." unless failed.empty?
end

desc "Regenerate result.pdf and firstpage.png of every example (or of one: rake regenerateqa[introduction/planets])"
task :regenerateqa, [:only] do |t, args|
  examples(args[:only]).each do |dir|
    run_xts(dir, "result")
    # The preview in the Readme tables: first page, 600 pixels wide.
    sh "pdftoppm", "-f", "1", "-l", "1", "-scale-to-x", "600", "-scale-to-y", "-1", "-png", "-singlefile", "result.pdf", "firstpage", chdir: dir.to_s
    rm_f Dir.glob(dir.join("result-*.xml").to_s)
    puts "regenerated #{rel(dir)}"
  end
end

desc "Remove the files a run or a comparison leaves behind"
task :clean do
  patterns = %w[xts.pdf xts-*.xml result-*.xml compare-report.html source-[0-9][0-9].png pagediff-[0-9][0-9].png result-[0-9][0-9].png]
  patterns.each { |p| rm_f Dir.glob(ROOT.join("**", p).to_s) }
end

task :default => :qa
