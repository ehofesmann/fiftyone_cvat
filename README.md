# CVAT Annotation Plugin

A plugin that contains utilities for integrating FiftyOne with the CVAT annotation integration backend
[described here](https://docs.voxel51.com/integrations/cvat.html).

## Installation

### Local Python environment:

```shell
fiftyone plugins download \
    https://github.com/ehofesmann/fiftyone_cvat
```

Refer to the [main README](https://github.com/voxel51/fiftyone-plugins) for
more information about managing downloaded plugins and developing plugins
locally.

Set the `FIFTYONE_CVAT_USERNAME=XXXXX`, `FIFTYONE_CVAT_PASSWORD=XXXXX`, and optionally `FIFTYONE_CVAT_URL=https://my.cvat.ai` environment variables following [these instructions](https://docs.voxel51.com/integrations/cvat.html#authentication).

### Install in FiftyOne Teams environment:

1) Download the zip of this repository:

![image](https://github.com/ehofesmann/fiftyone_labelbox/assets/21222883/2adb370b-e52e-4141-b7d0-3e39b502019f)

2) [Install it through your FiftyOne Teams App.](https://docs.voxel51.com/teams/teams_plugins.html#installing-a-plugin)

    (Alternative): Upload it through the [FiftyOne Teams management SDK.](https://docs.voxel51.com/teams/management_sdk.html#fiftyone.management.plugin.upload_plugin)

3) Add the `FIFTYONE_CVAT_USERNAME`, `FIFTYONE_CVAT_PASSWORD`, and optionally `FIFTYONE_CVAT_URL` [secrets in your FiftyOne Teams App.](https://docs.voxel51.com/teams/secrets.html)

## Usage

In the FiftyOne App, press `` ` `` or click the `Browse operations` action to open the Operators list. Select one of the operators mentioned below.

This plugin can also be used entirely through Python by loading the relevant methods directly from the plugin through `foo.get_operator()`.


### Operators

#### request_annotations

You can use this operator to create annotation tasks for the current dataset or
view.

This operator is essentially a wrapper around the
[request annotations Python workflow](https://docs.voxel51.com/user_guide/annotation.html#requesting-annotations):

```py
import fiftyone.operators as foo
annotate = foo.get_operator("@ehofesmann/cvat/request_annotations")
annotate(
    dataset_or_view,
    anno_key,
    label_schema=...,
    ...
)
```

where the operator's form allows you to configure the annotation key,
annotation backend, label schema, and any other applicable fields for your
annotation backend.

#### load_annotations

You can use this operator to load annotations for existing runs back onto your
dataset.

This operator is essentially a wrapper around the
[load annotations Python workflow](https://docs.voxel51.com/user_guide/annotation.html#loading-annotations):

```py
import fiftyone.operators as foo
load_annotations = foo.get_operator("@ehofesmann/cvat/load_annotations")

load_annotations(dataset, anno_key, ...)
```

where the operator's form allows you to configure the annotation key and
related options.

#### delete_annotation_run

You can use this operator to delete annotation runs.

This operator is essentially a wrapper around
[delete_annotation_run()](https://docs.voxel51.com/api/fiftyone.core.collections.html#fiftyone.core.collections.SampleCollection.delete_annotation_run):

```py
import fiftyone.operators as foo
delete_annotation_run = foo.get_operator("@ehofesmann/cvat/delete_annotation_run")

delete_annotation_run(dataset, anno_key, cleanup=True)
```

#### import_annotations

You can use this operator to load annotations for existing runs back onto your
dataset.

This operator is essentially a wrapper around the
[import_annotations method](https://docs.voxel51.com/user_guide/annotation.html#importing-existing-tasks):

```py
import fiftyone.operators as foo
import_annotations = foo.get_operator("@ehofesmann/cvat/import_annotations")

import_annotations(dataset, project_name="foo", data_path=data_map, ...)
```

**Note**: This operator is currently only supported for programatic exeuction.
The operator UI for App usage is not yet implemented.
