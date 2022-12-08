# Galvanicium

<https://app.galvanicium.org>

Galvanicium is a web application made to display and superimpose measurements
from potentiostats and battery cyclers.

The application supports the following file formats:
- [BioLogic](https://app.galvanicium.org/#?filelist=https%3A%2F%2Fzakodium-oss.github.io%2Fanalysis-dataset%2Fbigmap.json)

## Design of the application

The source code of Galvanicium is available on GitHub: <https://github.com/zakodium-oss/galvanicium-app>.

The Galvanicium application is build around 4 other open-source projects that we are developing and maintaining:

- [react-plot](https://github.com/zakodium-oss/react-plot): a ReactJS component designed to plot scientific data. You may be interested to check the interactive and [extensive documentation](https://react-plot.zakodium.com).
- [react-science](https://github.com/zakodium-oss/react-science): a set of ReactJS components and tools that allows to build scientific applications and that is also being used in [NMRium](https://github.com/cheminfo/nmrium).
- [filelist-utils](https://github.com/cheminfo/filelist-utils): a library that allows to deal with files that are coming either from the local drive using a drag and drop or from a web service.
- [biologic-converter](https://github.com/cheminfo/biologic-converter): a library that converts the proprietary BioLogic file format

## Loading data in Galvanicium

Currently, Galvanicium only supports the BioLogic file format (`.mps` `.mpr` and `.mpt` extensions).

It is possible to drag and drop a folder containing one or many experiments at once.
The files may also be zipped for convenience. They will be automatically decompressed when loading the data.

The second way to load the data is from a web service.

### Loading the data form a web service

The web service should provide 2 routes:

1. A route that provides the list of file to load
2. A route that returns the file

The first route should return a JSON array containing the list of all the available files.
For each file the following information is provided:

- `name`: name of the file
- `size`: size of the file (optional)
- `relativePath`: relative URL to load the file in which the baseURL is the URL that points to the TOC json file.
- `lastModified`: epoch (in ms) containing the date of last modification (optional)

Example:

`curl https://zakodium-oss.github.io/analysis-dataset/bigmap.json` returns:

```json
[
  {
    "name": "jdb11-1.mpr",
    "size": 2465718,
    "relativePath": "data/format/biologic/jdb11-1/jdb11-1.mpr",
    "lastModified": 1662726816877
  },
  {
    "name": "jdb11-1.mps",
    "size": 4330,
    "relativePath": "data/format/biologic/jdb11-1/jdb11-1.mps",
    "lastModified": 1662726816877
  },
  {
    "name": "jdb11-4.mpr",
    "size": 2041303,
    "relativePath": "data/format/biologic/jdb11-4/jdb11-4.mpr",
    "lastModified": 1662726816890
  },
  {
    "name": "jdb11-4.mps",
    "size": 9648,
    "relativePath": "data/format/biologic/jdb11-4/jdb11-4.mps",
    "lastModified": 1662726816891
  }
]
```

Once the TOC is loaded, queries will be made to load all the files for which the extension can be processed:

`curl https://zakodium-oss.github.io/analysis-dataset/data/format/biologic/jdb11-4/jdb11-4.mpr`

## Using Galvanicium

### Select one or many measurements

### Changing colors

### Zoom in / out

## General

### Funding

|                                             |                                                                                                                          |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| <img src="images/zakodium.svg" width="200"> | [Zakodium Sàrl](https://www.zakodium.com)                                                                                |
| <img src="images/bigmap.jpg" height="100">  | [Union’s Horizon 2020 research and innovation programme under grant agreement No 957189](https://www.big-map.eu/big-map) |

### License

[MIT](./LICENSE)
