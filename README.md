# ESV

Ruby library/gem for Excel generation with the ease of CSV generation.

Exporting CSVs because Excel generation is too complex? No more!

CSVs can be difficult to open correctly, e.g. in Excel on Mac.


## Usage

```
data = ESV.generate do |esv|
  esv << [ "Name", "Dogs", "Cats" ]
  esv << [ "Victor", 1, 4 ]
end

File.write("/tmp/test.xls", data)
```

### Ruby on Rails

In `config/initializers/mime_types.rb`:

```
Mime::Type.register ESV::MIME_TYPE, "xls"
```

As a model or whatever you prefer:

```
class MyExcelDocument
  def generate(name)
    ESV.generate { |esv| esv << [ "Hello #{name}" ] }
  end
end
```

Controller:

```
class MyController < ApplicationController
  include ESV::RailsController  # for send_excel

  def show
    data = MyExcelDocument.new("Rails").generate
    send_excel(data)
  end

  def another_example
    respond_to do |format|
      format.html { … }
      format.xls { send_excel(…) }
    end
  end
end
```


## Installation

Add this line to your application's Gemfile:

```ruby
gem 'esv'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install esv


## Credits and license

By Henrik Nyh for Auctionet.com under the MIT license.

Using [a lot of code](https://github.com/livingsocial/excelinator/blob/master/lib/excelinator/xls.rb) from LivingSocial's [Excelinator](https://github.com/livingsocial/excelinator), also under the MIT license.

This library is a thin wrapper around [Spreadsheet](https://github.com/zdavatz/spreadsheet) which does the heavy lifting.
