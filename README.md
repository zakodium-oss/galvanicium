# galvanicium

Galvanium is a react component that allows to visualize and superimpose

- [From Biologic file format](https://analysis-ui-components.pages.dev/#?filelist=https%3A%2F%2Fzakodium-oss.github.io%2Fanalysis-dataset%2Fbiologic.json)

## Design of the ReactJS component

The application is build around 4 other open-source projects that we are developing and maintaining:

- [react-plot](https://github.com/zakodium-oss/react-plot): a ReactJS component designed to display scientific information. You may be interested to check the interactive and [extensive documentation](https://react-plot.zakodium.com).
- [analysis-ui-component](https://github.com/zakodium-oss/analysis-ui-component): a set of ReactJS component that allows to build scientific applications and that is also being used in [NMRium](https://github.com/cheminfo/nmrium).
- [filelist-utils](https://github.com/cheminfo/filelist-utils): a library that allows to deal with files that are coming either from the local drive using a drag and drop or from a web service.
- [biologic-converter](https://github.com/cheminfo/biologic-converter): a library that converts the proprietary BioLogic file format

Internally Galvanicium has a state containing 3 properties:

- `data`: containing information related to data
- `view`: containing the information related to what is displayed in which module
- `prefs`: that will contain user defined preferences for the application

## Loading new data in the Galvanicium

Currently Galvanicium only supports the BioLogic file format `.mps` `.mpr` and `.mpt`.

It is possible to drag and drop a folder containing one or many experiments at once. The files may also be zipped for convenience, they will be automatically unzip when loading the data.

The second way to load the data is from a web service.

### Loading the data form a web service

The web service should provide 2 routes:

1. A route that provides the list of file to load
2. A route that returns the file

The first route should return a JSON containing the list of all the available files. For each file the following information is provided:

- `name`: name of the file
- `size`: size of the file (optional)
- `relativePath`: relative URL to load the file in which the baseURL is the URL that points to the TOC json file.
- `lastModified`: epoch (in ms) containing the date of last modification (optional)

Example:

`curl https://zakodium-oss.github.io/analysis-dataset/biologic.json` would return:

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

Once the TOC loaded queries will be done to load all the files for which the extension can be processed:

`curl https://zakodium-oss.github.io/analysis-dataset/data/format/biologic/jdb11-4/jdb11-4.mpr`

### Internals

Internally both approaches (drag/drop and web service) will generate a `FileCollection` (see https://cheminfo.github.io/filelist-utils/classes/FileCollection.html and https://github.com/cheminfo/filelist-utils).

To convert the various proprietary formats and add the parsed result to the application `data state` we will use `loaders`. A loader will receive a `FileCollection` and will try to parse what it can, often based on the file extension. An example of the `BioLogic` loader can be found [here](https://github.com/zakodium-oss/analysis-ui-components/blob/6f36ab05af11f848d4ed98eb10c99184a713ae97/src/app/data/loaders/biologicLoader.ts)

## Using Galvanicium

### Select one or many measurements

### Changing colours

### Zoom in / out

### Copy to clipboard

### Store / reload experiments

Galvanicium with store the data as a `.ium` that contains all the currently loaded data and that can be reloaded by drag / drop the file on the application.

### General

## Funding

|                                             |                                                                                                                           |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| <img src="images/zakodium.svg" width="200"> | [Zakodium sàrl](https://www.zakodium.com)                                                                                 |
| <img src="images/bigmap.jpg" height="100">  | [Union’s Horizon 2020 research and innovation programme under grant agreement No 957189](https://www.big-map.eu/European) |

## License

[MIT](./LICENSE)
