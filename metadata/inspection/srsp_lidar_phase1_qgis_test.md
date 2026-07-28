# SRSP LiDAR Phase 1 — QGIS /vsis3/ load test
Date: 2026-07-28

## Result: PASS

Loaded directly from R2 via GDAL /vsis3/ virtual filesystem.
Layer valid, canvas display correct — western margin strip visible,
basin interior blank as expected from 27.13% valid pixel stats.

## Environment required
export AWS_ACCESS_KEY_ID=<r2_key>
export AWS_SECRET_ACCESS_KEY=<r2_secret>
export AWS_S3_ENDPOINT=cab49a864db2c8fd50aa7f24700ed043.r2.cloudflarestorage.com
export AWS_VIRTUAL_HOSTING=FALSE
qgis &  # must launch from same terminal

## QGIS settings
Project CRS: EPSG:27700 — required to avoid on-the-fly reprojection warning
OSTN15 grid shift file not installed — set project CRS to 27700 as workaround

## URI used
/vsis3/wetlands-raw-rowan/montrose/srsp_lidar_phase1_dtm/2026-07-28__scotland-lidar-1-dtm/srsp_lidar_phase1_dtm_montrose.tif

## Python console command
uri = "/vsis3/wetlands-raw-rowan/montrose/srsp_lidar_phase1_dtm/2026-07-28__scotland-lidar-1-dtm/srsp_lidar_phase1_dtm_montrose.tif"
layer = iface.addRasterLayer(uri, "lidar_phase1", "gdal")
print(layer.isValid())  # returned True
