# Logstash

## Conf File 1 - Basic CSV Parsing:
```
input {
  file {
    path => "/path/to/csv/file.csv"
    start_position => "beginning"
    sincedbpath => "/dev/null"
  }
}

filter {
  csv {
    separator => ","
    columns => ["List", "Of", "Column", "Names", "Within", "CSV"]
  }
  mutate {
    rename => { "List" => "new.list" }
  }
}

output {
  elasticsearch {
    hosts => "http://localhost:9200"
    index => "Index Name Here"
  }
stdout {}
}
```
