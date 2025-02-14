# Interfacing with other applications

QWC2 offers a number of options to interface it with other applications.

## URL parameters <a name="url-parameters"></a>

The following parameters can appear in the URL of the QWC2 application:

- `t`: The active theme
- `l`: The layers in the map, see below.
- `bl`: The visible background layer
- `e`: The visible extent
- `c`: The center of the visible extent
- `s`: The current scale
- `crs`: The CRS of extent/center coordinates
- `hc`: If `c` is specified and `hc` is `true` or `1`, a marker is set at `c` when starting the application. Note: requires the `StartupMarkerPlugin` plugin to be active.
- `st`: The search text
- `hp`, `hf`, `ht`: Startup highlight parameters used in conjunction with the `qwc-fulltext-search-service`, see below.

The `l` parameter lists all layers in the map (redlining and background layers) as a comma separated list of entries of the form
```text
<layername>[<transparency>]!
```
where
- `layername` is the WMS name of a theme layer or group, or an external layer resource string in the format
```text
<wms|wfs>:<service_url>#<layername>
```
   for external layers, i.e. `wms:https://wms.geo.admin.ch/?#ch.are.bauzonen`.
- `<transparency>` denotes the layer transparency, betwen 0 and 100. If the `[<transparency>]` portion is omitted, the layer is fully opaque.
- `!` denotes that the layer is invisible. If omitted, the layer is visible.

*Note*: If group name is specified instead of the layer name, QWC2 will automatically resolve this to all layer names contained in that group, and will apply transparency and visibility settings as specified for the group.

The `urlPositionFormat` parameter in `config.json` determines whether the extent or the center and scale appears in the URL.

The `urlPositionCrs` parameter in `config.json` determines the projection to use for the extent resp. center coordinates in the URL. By default the map projection of the current theme is used. If `urlPositionCrs` is equal to the map projection, the `crs` parameter is omitted in the URL.

### Highlight feature on startup

If a search text passed via `st` results in a unique result, the viewer automatically zooms to this result on startup. If the search result does not provide a bounding box, the `minScale` defined in the `searchOptions` of the `TopBar` configuration in `config.json` is used.

When using the `qwc-fulltext-search-service`, you can hightlight a feature on startup as follows:
- Either specify `hp=<search product>&hf=<search filter>`
- Or specify `ht=<search text>&hp=<search product>`

See [Fulltext search](Search.md#fulltext-search) for more details.

## Launching external websites

QWC2 menu entries can be configured to launch external websites as described in [opening external websites](../configuration/ViewerConfiguration.md#opening-external-websites).

## Javascript API

The `API` plugin exposes many application actions via the `window.qwc2` object and makes them accessible for external applications. See [API plugin reference](../references/qwc2_plugins.md#api) for more details.

See [api_examples.js](https://github.com/qgis/qwc2-demo-app/blob/master/static/api_examples.js) for some concrete examples.

