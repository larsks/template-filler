# Template Filler

`template-filler` is a tool for rendering templates on the command
line.  It takes as input a [Jinja2][] template and a list of values on
the command line or in a configuration and produces the rendered
version of the template.

## Synopsis

    usage: filler [-h] [--key KEY] [--output OUTPUT] [--config CONFIG] template

    positional arguments:
      template

    optional arguments:
      -h, --help            show this help message and exit
      --key KEY, -k KEY
      --output OUTPUT, -o OUTPUT
      --config CONFIG, -f CONFIG

## Options

- `--key`, `-k` *key=value* -- Set *key* to *value*.  If *value*
  starts with a `[` or `{`, it will be parsed as a JSON value.
- `--config`, `-f` *config* -- Read template parameters, a [YAML][]
  format configuration file.
- `--output`, `-o` *output* -- Write output to *output* instead of
  *stdout*.

## Example

Given a template in `sample.txt.in` that looks like this:

    This is a list of people:

    {% for person in people %}
    - {{person.name}}

        Title: {{person.title}}
    {% endfor %}

And a parameter file `sample.yml` that looks like this:

    people:
      - { name: Alice,   title: "Chief muckamuck" }
      - { name: Bob,     title: "Grand pooba" }
      - { name: Mallory, title: "Llama herder" }

If you run this command:

    filler -p sample.yml sample.txt.in

You will get this output:

    This is a list of people:


    - Alice

        Title: Chief muckamuck

    - Bob

        Title: Grand pooba

    - Mallory

        Title: Llama herder

[jinja2]: http://google.com/
[yaml]: http://google.com/

