# frozen_string_literal:true

def write_markdown(file, year)
  dir = "./#{year}"
  Dir.mkdir dir unless Dir.exist? dir

  File.write("#{dir}/#{file}.md", %(---
layout: syllabus
course:
  term: Fall 2020
  number: IDST 270
  description: "Introduction to Digital Humanities"
  meetings:
  - location: TRIB 1213
    time: MWF 3 - 3:50
instructors:
- name: Deanna Stover
  email: deanna.stover@cnu.edu
  office:
  - hours: 
    location: online
---

# Schedule

{% include schedule.html %}

# Policies

{% include policies.md %}
))
end

def write_yaml(file)
  return if File.exist? "_data/#{file}.yml"

  File.write("_data/#{file}.yml", %(---
title: "Course Title"
start: 2020-08-15
end: 2020-11-20
holidays:
- date: 2020-11-25
  name: Reading Day
meets:
- monday
- wednesday
- friday
units:
- title: First Unit
  start: 1
weeks:
"1": First Week
classes:
- |
  * First Class
))
end

task :course do
  (ARGV[1..]).each do |file|
    task(file.to_sym) {}
    year = file[-4..]
    write_markdown(file, year)
    write_yaml(file)
  end
end

task :delete_course do
  (ARGV[1..]).each do |course|
    task(course.to_sym) {}
    year = course[-4..]
    FileUtils.rm "_data/#{course}.yml" if File.exist? "_data/#{course}.yml"
    FileUtils.rm "#{year}/#{course}.md" if File.exist? "#{year}/#{course}.md"
  end
end

task remove_course: :delete_course
