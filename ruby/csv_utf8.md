If you save with default csv, Excel display russian symbols not corrent
You need add BOM to start file

```ruby 
csv_content = CSV.generate(col_sep: "\t", encoding: 'utf-8') do |csv|
  csv << ["Русский текст", "English"]
end

write_content = Iconv.conv("utf-16le", "utf-8", "\xEF\xBB\xBF")
write_content += Iconv.conv("utf-16le", "utf-8", csv_content)
File.open("file.csv", 'wb') { |f| f.write(write_content) }
```

Thanks to http://stackoverflow.com/questions/451636/whats-the-best-way-to-export-utf8-data-into-excel/8131746#8131746
