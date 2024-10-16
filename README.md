# Poietic Tool

Command-line tool for manipulating and exploring Poietic Models, with support for
Stock and Flow simulation.

See also: [Full documentation](https://github.com/OpenPoiesis/PoieticTool/blob/main/Docs/Tool.md)
with all the commands.


## Installation

Available platforms: MacOS 14 (and later), Linux

To install the `poietic` command-line tool, run the following command in the
project's top-level directory:

```bash
./install
```

The tool will be installed in the Swift Package Manager's' `~/.swiftpm/bin`
directory. Make sure you have the directory in your `PATH`, if you do not, then
add the following to the end of your `~/.zshrc` or `~/.bashrc` file:

```bash
export PATH=~/.swiftpm/bin:$PATH
```

**Recommended** (optional): [Graphviz](https://graphviz.org) for visualising the design graph and [Gnuplot](http://www.gnuplot.info/docs_6.0/loc3434.html) for charts. The tool can generate output for both.

On MacOS with Homebrew:

```bash
brew install graphviz gnuplot
```

## Examples

The examples are located in the [Examples repository](https://github.com/OpenPoiesis/PoieticExamples).
Follow instructions how to run them in the documentation contained within the
repository.


## Tool Overview

The Poietic Flows includes a command-line tool to create, edit and run
Stock and Flow models called `poietic`.

See the [Command Line Tool documentation](Docs/Tool.md).

Command summary:

- `new`: Create an empty design.
- `info`: Get information about the design
- `list`: List design content objects.
- `show`: Describe an object.
- `edit`: Edit an object or a selection of objects.
    - `set`: Set an attribute value
    - `undo`: Undo last change
    - `redo`: Redo undone change
    - `add`: Create a new node
    - `connect`: Create a new connection (edge) between two nodes
    - `remove`: Remove an object – a node or a connection
    - `auto-parameters`: Automatically connect parameter nodes: connect required, disconnect unused
    - `layout`: Lay out objects
    - `align`: Align objects on canvas
- `import`: Import a frame into the design.
- `run`: Run the simulation and generate output
- `write-dot`: Write a Graphviz DOT file.
- `metamodel`: Describe the metamodel (supports: text, markdown and HTML output)
- `create-library` Create a library of multiple models.

Use `--help` with a desired command to learn more.

### Pseudo-REPL

Think of this tool as [ed](https://en.wikipedia.org/wiki/Ed_(text_editor)) but
for data represented as a graph. At least for now.

The tool is designed in a way that it is by itself interactive for a single-user. 
For interactivity in a shell, set the `POIETIC_DESIGN` environment variable to
point to a file where the design is stored.

Example session:

```
poietic new
poietic info

poietic edit add Stock name=water formula=100
poietic edit add Flow name=outflow formula=10
poietic edit connect Drains water outflow
poietic info

poietic list formulas

poietic edit add Stock name=unwanted formula=0
poietic list formulas
poietic edit undo

poietic list formulas

poietic run
```

Discover design possibilities by exploring the metamodel in a HTML file:

```
poietic metamodel -f html > metamodel.html
```

The above command will create a `metamodel.html` file with full description of
currently available metamodel for the given design.


## Features

- Preserved history – Editing is non-destructive and can be reversed
  using undo and redo commands.
- Exports to different formats:
    - [Graphviz](https://graphviz.org) dot files
    - CSV
    - Charts to [Gnuplot](http://gnuplot.info)



## See Also

- [Formulas](https://openpoiesis.github.io/PoieticFlows/documentation/poieticflows/formulas)
- [Metamodel](https://openpoiesis.github.io/PoieticFlows/documentation/poieticflows/metamodel)

Underlying packages:

- Poietic Core: [repository](https://github.com/openpoiesis/PoieticCore),
  [documentation](https://openpoiesis.github.io/PoieticCore/documentation/poieticcore/)
- Poietic Flows: [repository](https://github.com/openpoiesis/PoieticFlows),
  [documentation](https://openpoiesis.github.io/PoieticFlows/documentation/poieticflows/)


## Author

[Stefan Urbanek](mailto:stefan.urbanek@gmail.com)
