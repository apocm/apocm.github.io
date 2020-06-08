**Ruby**

**Libraries**
- SFTP: 'net/sftp'
- XML: 'nokogiri'
- CSV: 'csv'


Ruby Tricks

Here are some interesting things you can do with Ruby!

**Use the proc invocation shorthand when the invoked method is the only operation of a block.**

bad: names.map { |name| name.upcase } names.map { |name| name.id }

good: names.map(&:upcase) names.map(&:id)

**Favour unless over if for negative conditions.** 

bad: do_something if !some_condition

good: do_something unless some_condition

**Favour until over while for negative conditions.**

bad: do_something while !some_condition

good: do_something until some_condition

**Use ||= to initialize variables only if they are not already initialized. (Nb. Do not use for booleans)**

bad: name = name ? name : 'Pikachu'

bad: name = 'Pikachu' unless name

good - set name to 'Pikachu', only if it's nil or false: name ||= 'Pikachu'

**Use Hash#values_at when you need to retrieve several values consecutively from a hash.**

bad:email = data['email'] username = data['nickname']

good: email, username = data.values_at('email', 'nickname')

**Avoid using String#+ when you need to construct large data chunks. Instead, use String#<<. Concatenation mutates the string instance in-place and is always faster than String#+, which creates a bunch of new string objects.**

bad: 
```html = ''html += '<h1>Page title</h1>'```

good: 
```html = '' html << '<h1>Page title</h1>'```

**Prefer %w to the literal array syntax when you need an array of 2+ words.**

bad: STATES = ['draft', 'open', 'closed']

good: STATES = %w[draft open closed]

**gsub vs sub Don't use String#gsub in scenarios in which you can use a faster and more specialized alternative.**

url = 'http://example.com' str = 'lisp-case-rules'

bad: url.gsub('http://', 'https://') str.gsub('-', '_')

good: url.sub('http://', 'https://') str.tr('-', '_')

**Error Handling Good Practices**

**Use implicit begin blocks where possible.**

bad: 
`def foo
  begin
    # main logic goes here
  rescue
    # failure handling goes here
  end
 end`

good: `def foo # main logic goes here rescue # failure handling goes here end`

**Put more specific exceptions higher up the rescue chain, otherwise they will never be rescued from.**

bad: 
`begin # some code rescue StandardError => e # some handling rescue IOError => e # some handling that will never be executed end`

good:
`begin # some code rescue IOError => e # some handling rescue StandardError => e # some handling end`
