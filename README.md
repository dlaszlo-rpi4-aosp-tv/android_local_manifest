## AOSP Android 15 for Raspberry Pi 4 and Raspberry Pi 5

### How to build:

1. Establish Android build environment with Docker container:


Create the Android build directory:
```
mkdir ~/android
cd ~/android
```

Run the Docker container to set up the build environment:
```
docker run --privileged --device /dev/loop-control -v .:/home/builduser -e GIT_USERNAME="John Doe" -e GIT_EMAIL="john@example.com" --name aosp_builder -it dlaszlo/aosp_builder
```

At this point, you are inside the Docker container, in the `builduser` home directory, which is the same as the Android build directory you created and entered outside the container.

2. Initialize repo:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r10
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/dlaszlo-rpi4-aosp-tv/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
```

Or optionally, you can reduce download size by creating a shallow clone and removing unneeded projects:

```
repo init -u https://android.googlesource.com/platform/manifest -b android-15.0.0_r10 --depth=1
curl -o .repo/local_manifests/manifest_brcm_rpi.xml -L https://raw.githubusercontent.com/dlaszlo-rpi4-aosp-tv/android_local_manifest/android-15.0/manifest_brcm_rpi.xml --create-dirs
curl -o .repo/local_manifests/remove_projects.xml -L https://raw.githubusercontent.com/dlaszlo-rpi4-aosp-tv/android_local_manifest/android-15.0/remove_projects.xml
```

3. Continue from the original instructions at step 4: [raspberry-vanilla/android_local_manifest](https://github.com/raspberry-vanilla/android_local_manifest)  (Sync source code)
