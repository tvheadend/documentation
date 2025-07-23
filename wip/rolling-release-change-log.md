# Rolling Release Change Log

## Release: [4.3-2432\~g0af87f13f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2432*) (2025-07-21)

> transcode: add advanced options for deinterlacing
>
> This patch exposes additional configuration options for the deinterlace\_vaapi (hardware) and yadif (software) deinterlace filters:
>
> * Deinterlace rate type (rate): frame or field
> * Deinterlace fields only (auto): only deinterlace interlaced fields
> * VAAPI Deinterlace mode (mode): Bob, Weave, MADI, MCDI (for VAAPI only)
>
> These options allow the transcode deinterlace configuration to be fine-tuned. Most notably, the deinterlace filters can now be configured with field-rate deinterlacing, which causes (for example) 25fps interlaced input at a 90kHz timebase to produce 50fps output with a 180kHz timebase.
>
> To maintain MPEG-TS compliance, the output timebase is fixed at 90kHz, and both the adjusted output frame rate (e.g. 50fps) and frame timestamps are rescaled accordingly before encoding. For accuracy, this rescaling is performed dynamically using libav functions such as av\_rescale\_q(), based on the timebase of the final filter in the AVFilterContext chain and the timebase of the output AVCodecContext. This approach supports fractional frame rates and remains robust against future changes to the filter configuration, including various combinations of deinterlace options.
>
> When field-rate deinterlacing is selected, this produces frames with (for example) correct timing of 50fps playback in a 90kHz container, ensuring that the transcoded output stream preserves the intended cadence and temporal fidelity of the original interlaced source.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0af87f13f786046df7bb610f8a6b291c26af1b14) (2025-07-21)

***

## Release: [4.3-2431\~gb9d34f913](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2431*) (2025-07-20)

> move filter\_hw\_denoise and filter\_hw\_sharpness to tvh\_codec\_profile\_video
>
> fixes: https://github.com/tvheadend/tvheadend/issues/1818 also fixes a logical define bug: filter\_denoise and filter\_sharpness should be transferred for all HW accels (not only for VAAPI)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b9d34f9135a0b40405581e7dd6534d97327f86eb) (2025-07-20)

***

## Release: [4.3-2430\~gda9fa6032](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2430*) (2025-07-18)

> Add Season number and Episode number to file name formatting strings.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/da9fa60323a972f66ac3adf5800ef78f571fba82) (2025-07-18)

***

## Release: [4.3-2428\~ge065d661a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2428*) (2025-07-17)

> Implement age ratings on XMLTV
>
> Update xmltv.c
>
> Apply suggestion from @Copilot
>
> Test for epgdb\_processparentallabels to avoid false positives
>
> Add branch in case rating\_label exists but system is null
>
> Fallback to rl\_display\_age before rl\_age
>
> Co-Authored-By: Copilot [175728472+Copilot@users.noreply.github.com](mailto:175728472+Copilot@users.noreply.github.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/e065d661aa837aef0fa93b5350afef4a2b77ed79) (2025-07-16)

***

## Release: [4.3-2429\~g5ff6128c7](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2429*) (2025-07-17)

> Add Scene Markers to recordings at scheduled EPG event start/stop times.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/5ff6128c7468f3606bb1f0622422878ad39a7c45) (2025-07-17)

***

## Release: [4.3-2427\~gaaf31d964](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2427*) (2025-07-16)

> Fix builds on debian buster

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/aaf31d96422bad6474744e2bddc65451b2c6b96a) (2025-07-16)

***

## Release: [4.3-2426\~gd1fb6da0a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2426*) (2025-07-12)

> Fix broken squash-autocomment

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/d1fb6da0a3a4583d9bb125276bb680ab7b2b87fe) (2025-07-11)

***

## Release: [4.3-2425\~gd431956cc](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2425*) (2025-07-05)

> Add 'sudo make install' to the Linux build notes.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/d431956cc62f80115fa17103374f7c921081d72c) (2025-07-05)

***

## Release: [4.3-2424\~gbfcc00142](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2424*) (2025-07-03)

> Cloudsmith supports fedora 42 now

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/bfcc001423c1ae423ce67e8e35ca702c65f994b2) (2025-07-03)

***

## Release: [4.3-2423\~gea3d32791](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2423*) (2025-06-27)

> Update coverity secret check to new ENV file

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ea3d32791b94c9a9285920d8cc1396eb3db2b52c) (2025-06-27)

***

## Release: [4.3-2422\~g61d728e1a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2422*) (2025-06-21)

> Update online help text
>
> Format Strings used in DVR Profiles cannot be used when creating Autorecs. See Forum issue 9160.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/61d728e1a4bd3e35653a902bf82e3b57c5564013) (2025-06-21)

***

## Release: [4.3-2421\~g730718c28](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2421*) (2025-06-12)

> fix memory leak 3 - transcoding
>
> * fix memory leak 3 - transcoding

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/730718c2888a121a00b96f3460b2e8f5ca8396d1) (2025-06-12)

***

## Release: [4.3-2418\~gf7edaf48c](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2418*) (2025-06-10)

> Recognize checkbox for feature proposals properly

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/f7edaf48cbe2e068e2126a6b355ae64b2d1b1f6e) (2025-06-10)

***

## Release: [4.3-2419\~g7bbbe57e9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2419*) (2025-06-10)

> User's DVR Configuration profile not used when scheduling recordings via HTSP

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7bbbe57e9ebb204e1070b219fda611be91bb0ae0) (2025-06-10)

***

## Release: [4.3-2420\~g19026f320](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2420*) (2025-06-10)

> remove coded\_width and coded\_height from encoding
>
> according to AVCodecContext documentation this is only used for decoding, oavctx is used for encoding

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/19026f3202fbacb8ddd89b13d358ee64ce7f4929) (2025-06-10)

***

## Release: [4.3-2417\~g42ed6affc](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2417*) (2025-06-09)

> Add missing coverity env

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/42ed6affc42ef06e427fb8b1465532a4489e182c) (2025-06-09)

***

## Release: [4.3-2416\~g09a06f11a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2416*) (2025-06-09)

> Fix coverity builds

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/09a06f11acf0d3957b6dfa08f13b48f7bd1262fd) (2025-06-09)

***

## Release: [4.3-2414\~gc4ce95ab9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2414*) (2025-06-06)

> repo: cleanup CONTRIBUTING.md
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c4ce95ab9603e0ceaccf868690aad7414af5cd95) (2025-06-06)

***

## Release: [4.3-2412\~gaadcc3a8d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2412*) (2025-06-06)

> intl: js: change freenode to Libera.Chat
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/aadcc3a8d946ad28e33cf721880abe4709bd44bc) (2025-06-06)

***

## Release: [4.3-2415\~g56d23c872](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2415*) (2025-06-06)

> ci: disable coverity on forks
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/56d23c8725b0563587eda0ccaed93153fa77505c) (2025-06-06)

***

## Release: [4.3-2410\~g808a87a6a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2410*) (2025-06-04)

> HTSP: Expose is\_new flag in EPG event data
>
> This commit adds the is\_new flag to the EPG event data sent to HTSP clients. By including this property, clients such as Kodi (with the pvr.hts addon) can now detect whether a broadcast is marked as new and set corresponding flags (e.g. EPG\_TAG\_FLAG\_IS\_NEW in Kodi).
>
> This enhances the metadata available to clients and supports improved EPG event handling and display.
>
> A corresponding pull request will also be submitted to the pvr.hts project to make use of this flag when obtaining EPG event guide data from Tvheadend.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/808a87a6aa6eeabd4be3a024e4eea023aaf00cf6) (2025-06-04)

***

## Release: [4.3-2409\~g0f74b0ab0](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2409*) (2025-06-04)

> Coverity CID 552897

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0f74b0ab0a3b96d87da04d9c778142ecfb370a1d) (2025-06-04)

***

## Release: [4.3-2405\~g8d469350f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2405*) (2025-06-02)

> Add API call 'status/activity'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8d469350fa67cb1ce923ecaf303d5ba3bf5c1518) (2025-06-02)

***

## Release: [4.3-2408\~g85360924d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2408*) (2025-06-02)

> transcode: gracefully handle common hardware decoder errors
>
> When using VAAPI hardware decoding, certain malformed or corrupt frames at the start of the stream may cause the ffmpeg h/w decoder to emit `AVERROR(EIO)` or `AVERROR(EINVAL)` early in the picture decoding phase.
>
> In these cases, libav will log errors such as:
>
> \[ ERROR]:libav: AVCodecContext: Failed to upload decode parameters: 18 (invalid parameter). \[ ERROR]:libav: AVCodecContext: Failed to end picture decode after error: 18 (invalid parameter). \[ ERROR]:libav: AVCodecContext: hardware accelerator failed to decode picture
>
> Currently, Tvheadend treats these errors as fatal, resulting in the transcoder stream being torn down via `tvh_stream_stop()` and interrupting client playback, typically leaving only audio and a black screen.
>
> While this behavior is somewhat tolerable during live TV viewing—where the user can manually resolve the issue by changing channels—it is significantly more disruptive in recording scenarios, as it results in recordings containing only audio and no video.
>
> However, when the same streams are run directly through FFmpeg’s CLI, FFmpeg **does not abort** on these errors — it logs them and continues transcoding. This makes FFmpeg's failure handling more robust than Tvheadend's.
>
> To identify which errors should be considered recoverable, the transcoder was instrumented to log the exact `AVERROR` codes encountered during decoding failures. A stress test was then run using a channel-hopping script that switched channels every 5 seconds over several hours. The failure rate was approximately 1%, and in **all** cases, the decoding failures were either `AVERROR(EIO)` or `AVERROR(EINVAL)`. Allowing the stream to continue after these specific errors proved effective — playback resumed, and only a minor picture glitch was visible at the affected frame, with no need to tear down the video stream.
>
> This patch updates `tvh_context_decode()` to include `AVERROR(EIO)` and `AVERROR(EINVAL)` in the list of tolerated decode errors, aligning Tvheadend's behavior with FFmpeg’s more forgiving approach.
>
> FFmpeg’s internal decoder logic in `vaapi_h264.c` and `decode.c` supports this tolerance model. For example, in `decode_simple_internal()` and `submit_frame()`, errors like `EIO` may occur during `av_hwframe_transfer_data()` or `vaEndPicture()`, but are **not considered fatal**. Instead, FFmpeg logs the issue and decoding continues on the next frame.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/85360924d0e215c2ba0b1b224e3111be712eae0f) (2025-06-02)

***

## Release: [4.3-2406\~g128854638](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2406*) (2025-06-02)

> fix for video stream detection
>
> PR https://github.com/tvheadend/tvheadend/pull/1772 is not covering all video streams. The proper implementation is to use the macro SCT\_ISVIDEO()

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/1288546386ae775200083ff0788dcdb8d783ce46) (2025-06-02)

***

## Release: [4.3-2404\~gc0c55c783](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2404*) (2025-05-27)

> fix memory leak 2 - transcoding
>
> fix memory leak 2 - transcoding

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c0c55c7838ae505c04e90be16da9919b6d49a146) (2025-05-27)

***

## Release: [4.3-2403\~g532c2a71f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2403*) (2025-05-27)

> fix dead error condition
>
> Fixes coverity scan issues: 462150

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/532c2a71f2f7ad938e6763db2f0f3013863fffc0) (2025-05-27)

***

## Release: [4.3-2402\~gede23be0d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2402*) (2025-05-26)

> add mpegts parameters from input stream
>
> * add service\_name, service\_provider, mpegts\_transport\_id, mpegts\_service\_type, mpegts\_pmt\_start\_pid, mpegts\_start\_pid, mpegts\_service\_id, mpegts\_original\_service\_id
> * allow user to select mpeg ts sid (same like pass profile)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ede23be0d25fc7d42f144fec551e4742f082a37c) (2025-05-25)

***

## Release: [4.3-2401\~g27b12a92d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2401*) (2025-05-25)

> fix memory leak - transcoding
>
> Fixes coverity scan issues: 551230, 551229, 507422 and 507421

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/27b12a92d04d5120b9e61f16e620d496d18d6f6d) (2025-05-25)

***

## Release: [4.3-2400\~g1a3ca885a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2400*) (2025-05-25)

> Fix recording thread freeze when unable to create unique file name.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/1a3ca885a4706b57cb9326663955176f72804376) (2025-05-25)

***

## Release: [4.3-2399\~g26a14aa31](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2399*) (2025-05-23)

> MKV Tags - Change rating label. Add Sub-title and Comment.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/26a14aa318a631a9f96008215e63efd6d6132727) (2025-05-23)

***

## Release: [4.3-2398\~g7e1f9caa9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2398*) (2025-05-22)

> fix memory leak
>
> Fixes: https://github.com/tvheadend/tvheadend/issues/1749

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7e1f9caa95bf8d3d3e5c3a5eb687e7acf5b9a916) (2025-05-22)

***

## Release: [4.3-2397\~gebac08749](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2397*) (2025-05-20)

> video hw accel should only be applied for video streams
>
> Fixes: https://github.com/tvheadend/tvheadend/issues/1827

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ebac08749e1272e41ac94aadce8a4d716da3a779) (2025-05-20)

***

## Release: [4.3-2395\~g75119b6e9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2395*) (2025-05-19)

> Update VAAPI transcoding as recommended by ffmpeg 6.1.1/doc/examples/… (#1792)
>
> Update VAAPI transcoding as recommended by ffmpeg 6.1.1/doc/examples/vaapi\_\*.c

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/75119b6e9640992cefe67cc3b45025367df7071e) (2025-05-19)

***

## Release: [4.3-2396\~g36ba82848](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2396*) (2025-05-19)

> Add Sub-Title Processing Options for DVB OTA EPG

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/36ba82848bc1837a9b9ee790219ae38e1228b576) (2025-05-19)

***

## Release: [4.3-2394\~g7da199b61](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2394*) (2025-05-18)

> update audio abuffersink from deprecated channel\_layouts to ch\_layouts and deprecated FF\_PROFILE\_\* --> AV\_PROFILE\_\*
>
> update audio abuffersink from deprecated channel\_layouts to ch\_layouts and deprecated FF\_PROFILE\_\* --> AV\_PROFILE\_\*

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7da199b61cb2589d65100d55bb736c378ad7c125) (2025-05-18)

***

## Release: [4.3-2393\~g221400c9f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2393*) (2025-05-17)

> iptv: handle relative key URL

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/221400c9f2d41e974cc8f96269e65c1b2e20dce1) (2025-05-17)

***

## Release: [4.3-2392\~g03272650d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2392*) (2025-05-15)

> \[Docker]: Tag alpine master as latest

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/03272650dd6cc071163baeb03182bb77c249f024) (2025-05-15)

***

## Release: [4.3-2390\~gcf2929259](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2390*) (2025-05-14)

> allow NVENC, VAAPI and MMAL to coexist in the same build
>
> * allow NVENC, VAAPI and MMAL to coexist in the same build.
> * give the user the capability for prioritize hw decoder or to match the hw decoder with hw encoder
> * refactor source code: remove duplicate source code in codec.js

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/cf29292592756f778024b3f5d8df166dad899285) (2025-05-14)

***

## Release: [4.3-2388\~gcebe61590](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2388*) (2025-05-14)

> wizard: increase buffer size to silence -Wformat-truncation on GCC 15
>
> GCC 15.1 introduces stricter checks around `snprintf`-like functions under `-Wformat-truncation`, even when the format string itself is under developer control. This triggers a false positive in `hello_changed()` when building with `-Werror=format-truncation`:
>
> error: ‘\_\_builtin\_\_\_snprintf\_chk’ output may be truncated before the last format character \[-Werror=format-truncation=]
>
> note: output between 1 and 33 bytes into a destination of size 32
>
> This warning is triggered due to a theoretical edge case in `tvh_strlcatf()` where combining strings like `"en,fr,de"` could approach the buffer limit of 32 bytes. While truncation is unlikely in practice, the warning is still emitted aggressively by the new FORTIFY logic.
>
> Increase the buffer from 32 to 64 bytes to silence the warning and ensure headroom. This avoids having to disable the diagnostic, while still keeping the logic and usage intact. This is a defensive fix with no behavioral change, and aligns with similar mitigations used in other projects facing the same issue with GCC >= 13 and especially 15+.
>
> Tested with GCC 15.1.1, built cleanly.
>
> Refs:
>
> * https://gcc.gnu.org/bugzilla/show\_bug.cgi?id=108231
> * https://gcc.gnu.org/onlinedocs/gcc-15.1.0/gcc/Warning-Options.html#index-Wformat-truncation

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/cebe6159042c0782cbe22d26446b141fa07d43b8) (2025-05-13)

***

## Release: [4.3-2391\~gbdec3c501](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2391*) (2025-05-14)

> fix read/write of PT\_DYN\_INT
>
> PT\_DYN\_INT should be read and write as int (32 bits)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/bdec3c501fe4ef6d5d8c1d94c3ba733ddb7e391c) (2025-05-14)

***

## Release: [4.3-2389\~g13804ab50](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2389*) (2025-05-14)

> Show recording file name

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/13804ab50ce41d81b987d97f050942efe49c4792) (2025-05-14)

***

## Release: [4.3-2387\~gdf4eaf8e1](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2387*) (2025-05-13)

> Fix crash when updating 'disp\_summary'

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/df4eaf8e1913028c5cccd6320e462069382b6720) (2025-05-13)

***

## Release: [4.3-2382\~gda1ac73b9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2382*) (2025-05-13)

> Global setting for 'Items per page'

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/da1ac73b92f1b9426bcf08dc7f8d2746cf139bb9) (2025-05-13)

***

## Release: [4.3-2379\~gcc07e3471](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2379*) (2025-05-13)

> lovcombo-all.js: Fix autorec create/edit TypeError with Firefox 134 (#1786)
>
> Firefox 134 added the RegExp.escape() method (https://tc39.es/proposal-regex-escaping/#sec-regexp.escape) with a standards-compliant implementation that throws TypeError if any value other than a String is passed in. This differs from the existing polyfill that simply returns the argument unmodified if it isn't a String. In TVHeadend, the day-of-the-week selector (as used in the Autorec and Timer configuration) uses Integers as keys for options, causing an Integer to get passed to RegExp.escape() on line 300 of lovcombo-all.js. Because of the non-standards- compliant permissive behavior of the polyfill, this previously didn't cause an issue. However, with Firefox 134 (and an upcoming version of Safari), the added standards-compliant method causes a TypeError to be thrown on every attempt to create or edit a timer or autorec, causing the edit window to not be shown. To solve the issue, pass the response from r.get(this.valueField) through the String() constructor to ensure anything that gets passed in is a String. This has been tested with Firefox and Chrome with both Integer and String keys.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/cc07e3471e314469dca3086f134bf3384e06fc83) (2025-05-13)

***

## Release: [4.3-2386\~gba243eaf3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2386*) (2025-05-13)

> Translation for 'en\_US' updated. intl: Translate tvheadend.doc.pot in en\_US
>
> 100% translated source file: 'tvheadend.doc.pot' on 'en\_US'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ba243eaf3eb8b70f765ae6d4ad3f33bd18e50a9a) (2025-05-13)

***

## Release: [4.3-2378\~gab81dce3e](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2378*) (2025-05-13)

> Fix Cloudsmith uploads

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ab81dce3ebfef30626a8ddf3f9a68b6bdd4f47ba) (2025-05-12)

***

## Release: [4.3-2380\~g728885fbe](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2380*) (2025-05-13)

> httpc.c: Fix HTTPS with OpenSSL 3.5 (#1813)
>
> The TLS Client Hello message is larger in OpenSSL 3.5 and will not fit in the previous hc\_io\_size of 1024 bytes. This causes the TLS Client Hello message to be truncated, resulting in HTTPS requests stalling and eventually timing out. To fix this, increase hc\_io\_size to 2048 bytes.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/728885fbe3019c6896efc474c8cf336bfadaeea5) (2025-05-13)

***

## Release: [4.3-2381\~g0eea8a59f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2381*) (2025-05-13)

> Remove links to old Wiki (#1793)
>
> * Remove links to old Wiki. Fixes #1660 Also remove references to CIC and CLA, and other content where a more recent version exists on the documentation site.
> * Remove more obsolete links.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0eea8a59f0834e2a3babdd8028c02509428a097c) (2025-05-13)

***

## Release: [4.3-2375\~g653bd0400](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2375*) (2024-11-13)

> Check for hidden fields before reading them. Fixes #1782.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/653bd0400b4413db96b80c807f0f7524f9248adb) (2024-11-12)

***

## Release: [4.3-2372\~gb69dac929](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2372*) (2024-10-08)

> iptv: allow to limit UDP ports for unicast inputs

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b69dac9299fde5fd43200a9a56c43bba1ce145cf) (2024-10-08)

***

## Release: [4.3-2374\~g26ec161fb](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2374*) (2024-10-08)

> Translation for 'en\_US' updated. intl: Translate intl/tvheadend.pot in en\_US
>
> 100% translated source file: 'intl/tvheadend.pot' on 'en\_US'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/26ec161fb3c903f8b0d0be8b54d1b67c596fb829) (2024-10-08)

***

## Release: [4.3-2371\~geee5cdadf](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2371*) (2024-10-05)

> update libvpx v.1.14.1
>
> update libvpx v.1.14.1 remove previous patch (from 1.14.0)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/eee5cdadf244b80efddedb944a55c9cdbb0ff6c9) (2024-10-05)

***

## Release: [4.3-2370\~g28de5c092](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2370*) (2024-09-28)

> Fix - Audio transcoding not working #1663
>
> src/transcoding/transcode/helpers.c : pktbuf\_len(self->input\_gh)) will be 0 (empty) so will return error -11 (AVERROR(EAGAIN) for audio streams.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/28de5c092c657ffbbffa422c2ca3c07ba513c567) (2024-09-28)

***

## Release: [4.3-2369\~g05c3170ae](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2369*) (2024-09-28)

> Add start timeout to streaming profile
>
> This allows overriding the hardcoded grace period of 20 seconds. It should address the problems described in \[1]\[2].
>
> In addition, timeout code has been slightly refactored for readability and more debug logging.
>
> \[1] https://tvheadend.org/d/8330-increase-timeout-when-tuning-iptv-mux/2 \[2] https://tvheadend.org/d/8158-several-problems-questions-about-using-tvheadend-starting-with-not-waiting-long-enoough-for-stream-to-begin

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/05c3170aef2d28136e34ba6b95afbbb57916e4d7) (2024-09-28)

***

## Release: [4.3-2367\~g9dec5b585](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2367*) (2024-09-23)

> fixes #1733

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/9dec5b585d8c1b4bb8ae8890985cc5a0148de24f) (2024-09-23)

***

## Release: [4.3-2368\~g55404da6c](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2368*) (2024-09-23)

> Remove HTSP client version test for rating labels and string UUIDs

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/55404da6cfd3b0dbbfd5982f87d31dc41f93f509) (2024-09-23)

***

## Release: [4.3-2366\~g9ac57a0c1](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2366*) (2024-09-06)

> bouquet: fix overzealous channel removals in merged multi-network setup

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/9ac57a0c1a4551012260008cfca6bfc2386f6dcf) (2024-09-06)

***

## Release: [4.3-2364\~g4aff54328](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2364*) (2024-09-06)

> HTSP: deliver 'comment' with autorecEntry(Add|Update), timerecEntry(Add|Update). Allow setting 'comment' with 'updateDvrEntry'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/4aff543283b88017a59c90ccd7d22aee24b5ee4f) (2024-09-06)

***

## Release: [4.3-2365\~g2e92208c3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2365*) (2024-09-06)

> Fixup updating comment in \_dvr\_entry\_update. Only overwrite existing title if comment is not NULL. Follows the same logic now as other updates done in this function.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2e92208c3c97672efad3b5d65889a048bbebdea1) (2024-09-06)

***

## Release: [4.3-2363\~g18ff23f90](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2363*) (2024-09-06)

> Add country and authority to HTPS messages containing rating labels.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/18ff23f909d8b5c27e9e209c7e50bc5bddce9da2) (2024-09-06)

***

## Release: [4.3-2361\~gdd82541c4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2361*) (2024-08-28)

> HTSP: Expose DVR configuration id in 'dvrEntryAdd', 'dvrEntryUpdate', 'autorecEntryAdd', 'autorecEntryUpdate', 'timerecEntryAdd', 'timerecEntryUpdate'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/dd82541c4c4c372a5b6af15e3dc0477f75c1b1bd) (2024-08-28)

***

## Release: [4.3-2359\~gfc5a1672e](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2359*) (2024-08-25)

> HTSP: Expose broadcast type in 'autorecEntryAdd' and 'autorecEntryUpdate'. Handle broadcast type in 'addAutorecEntry' and 'updateAutorecEntry'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/fc5a1672e083155193f3daf697748780f0d02aa9) (2024-08-25)

***

## Release: [4.3-2360\~g266d03527](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2360*) (2024-08-25)

> Fix mapping HTSP field 'broadcastType' to internal field. Must be 'btype'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/266d03527936ea0d65e6edb06010cd91847493ab) (2024-08-25)

***

## Release: [4.3-2358\~gfacbd4e4b](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2358*) (2024-08-24)

> Fix FTBFS introduced by 76d8fc8bc5455322558c764c84755ebbba254ad5
>
> Older versions of GCC don't like declaring a variable in the middle of a switch/case and will fail with "error: a label can only be part of a statement and a declaration is not a statement".

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/facbd4e4b79f6175daa45bfe5d724b8304648c12) (2024-08-24)

***

## Release: [4.3-2357\~g3bb78afa4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2357*) (2024-08-23)

> fix bug in AAC channel layout configuration tab
>
> fix bug in AAC channel layout configuration tab There are few issues:
>
> 1. first entry in combo should be AUTO (with value 0) - in original code was set to 1 (and overwritten later)
> 2. l->nb\_channel is not the best way to cycle though layouts available. At the end I think is accessing some region outside of the struct (because I see is lopped also after 7.1). The way I knew how to fix was to add the filter (l->nb\_channels < 32). Maybe changing the while to for will be a better option.
> 3. av\_channel\_layout() is returning the length of the string ... we should use l\_buf only when retuned value > 0 ... when is < 0 l\_buf was not updated.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/3bb78afa456f6f430827450612b67f53f9cd211e) (2024-08-23)

***

## Release: [4.3-2356\~g267aef151](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2356*) (2024-08-23)

> HTSP: Expose service provider name with channel information.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/267aef151ec30fa9c5469500100ab7f59092d39a) (2024-08-22)

***

## Release: [4.3-2355\~gf20e38dae](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2355*) (2024-08-22)

> Update Fedora versions for cloudsmith uploads

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/f20e38daeb6a9727b24923eb77da2a35a96d8a3f) (2024-08-22)

***

## Release: [4.3-2354\~gadef81b8d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2354*) (2024-08-12)

> Update linuxdvb\_satconf.c - lnb poweroff requires power save
>
> Extend description to make it clear that lnb\_poweroff also requires "power save" setting.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/adef81b8d2a6edb3a665679f394bac05b7dc91c8) (2024-08-12)

***

## Release: [4.3-2353\~g76d8fc8bc](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2353*) (2024-08-12)

> update vaapi - vainfo
>
> * add enable vainfo detection checkbox in config
> * defined PT\_DYN\_INT to load integer field from function
> * PT\_DYN\_INT must be paired with dyn\_i
> * show only VAAPI codecs advertised by vainfo
> * defined two invisible fields: ui and uilp used for UI enable/disable features
> * check if bitrate is greater than max\_bitrate (fix to avoid tvh crash)
> * vp8, vp9 separate Global Quality from Quality
> * load quality and max B frames filters from vainfo
> * UI has several constrains or warnings implemented using vainfo
> * separated 'b\_depth' from 'bf'

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/76d8fc8bc5455322558c764c84755ebbba254ad5) (2024-08-12)

***

## Release: [4.3-2352\~g49ac93871](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2352*) (2024-08-10)

> Enforce issue templates on GitHub

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/49ac9387186d32b55a399a04155e835eac22c6c1) (2024-08-10)

***

## Release: [4.3-2351\~g078a822cf](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2351*) (2024-08-04)

> Replace deprecated channels/channel\_layout

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/078a822cf548b37bc474475fa57e48e9604090ee) (2024-08-04)

***

## Release: [4.3-2349\~gb774bdd25](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2349*) (2024-07-21)

> Translation for 'en\_US' updated. intl: Translate intl/js/tvheadend.js.pot in en\_US
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'en\_US'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b774bdd25351e51eba0282ccf7c65904dc1b5655) (2024-07-21)

***

## Release: [4.3-2347\~g1dc8ffe78](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2347*) (2024-07-14)

> Rework fullscreen request method detection

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/1dc8ffe781b688f6ba7bacddd518399ea289efa6) (2024-07-13)

***

## Release: [4.3-2346\~g457c02d30](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2346*) (2024-07-13)

> Add dependency for recent Fedora versions

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/457c02d305d92a5036c6d3406f64e03de9ac235a) (2024-07-13)

***

## Release: [4.3-2344\~gd2e41b553](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2344*) (2024-06-27)

> Remove tvheadend user on purge
>
> This fixes #1722 on my test system.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/d2e41b553e7cc6eb06fd21b42bbed4b3a1f28bc0) (2024-06-27)

***

## Release: [4.3-2343\~g1644b6e15](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2343*) (2024-06-27)

> Refactor null value handling.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/1644b6e15738490c337a50d2b46fa4e9eb0a18e5) (2024-06-27)

***

## Release: [4.3-2342\~g128d6861f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2342*) (2024-06-25)

> Replace deprecated interlaced\_frame, top\_field\_first and key\_frame

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/128d6861fac67ea6638c2956d092a46e23eb8988) (2024-06-25)

***

## Release: [4.3-2338\~gfd61453da](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2338*) (2024-06-23)

> Remove useless NULL-assignment in http.c
>
> Found by coverity

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/fd61453da3118c174cadca9cec1ee1d49f0a1548) (2024-06-23)

***

## Release: [4.3-2339\~gcd6bfbb0b](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2339*) (2024-06-23)

> Fix potential null-pointer dereference in muxer\_mkv.c

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/cd6bfbb0bb45e7a22690f3d82183125f2b105cfd) (2024-06-23)

***

## Release: [4.3-2340\~gc8435a098](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2340*) (2024-06-23)

> Remove useless NULL-check in ratinglabels.c
>
> Found by coverity

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c8435a0985ca66a9bd12f33703c8f76c95ddea43) (2024-06-23)

***

## Release: [4.3-2337\~ge855f62e6](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2337*) (2024-06-18)

> Use safer htsmsg\_add\_str2 when copying de->de\_directory
>
> de->de\_directory may be null. htsmsg\_add\_str passes str unchecked to underlying strlen function. \_\_strlen\_avx2 will segfault if str is null.
>
> htsmsg\_add\_str2 checks the value of args before passing them to htsmsg\_add\_str, which should prevent this.
>
> Fixes #1712

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/e855f62e6697cf756ad2eed2ed03b8d06ba2019b) (2024-06-18)

***

## Release: [4.3-2336\~g366e56290](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2336*) (2024-06-15)

> XMLTV: Rating Labels: Use 'NONE' when 'system' attribute is missing

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/366e5629057e39de68932a0a0613a8af14076e31) (2024-06-15)

***

## Release: [4.3-2335\~gf15f05761](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2335*) (2024-06-07)

> Allow setting a custom grace period for LinuxDVB adapters
>
> When using Astrometa to tune to DVB-T2 muxes in Poland, the scans are reported as complete but the found services have zero elementary services due to the scan period being too short in order to fetch PMTs.
>
> This change allows overriding the default grace period of 5 seconds with a custom value. I successfully scanned all services with this setting changed to 15 for this particular adapter/mux combination.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/f15f05761fb713fb9d754e94fc92253922fc4357) (2024-06-06)

***

## Release: [4.3-2327\~ge6b1d5ffb](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2327*) (2024-06-06)

> Extend CORS origin help/hover message
>
> Clarify that the value should be a URL, prefixed with http:// or https://, and not "bare" domains, which currently silently fail to save. Fixes (partially) #1700.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/e6b1d5ffbaa59956aeea7a9ace2410638cbcc211) (2024-06-06)

***

## Release: [4.3-2326\~g6c5c8eae4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2326*) (2024-06-06)

> dvr: Added missing directory to rerecord-entry
>
> Previously if you had a directory set on a recording and this recording needed to be rerecorded, the directory was not kept in the new entry.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/6c5c8eae494943b7749b3fc9ee58a30ab1983bf4) (2024-06-06)

***

## Release: [4.3-2334\~g552f9414e](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2334*) (2024-06-06)

> Always compile x265 as PIC

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/552f9414e26f1d1d80440881da44c24db6968b5d) (2024-06-06)

***

## Release: [4.3-2325\~g3ac184725](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2325*) (2024-06-06)

> tvhdhomerun: Add ISDB to type check in tvhdhomerun\_device\_create
>
> This commit adds support for ISDB in the type check of the tvhdhomerun\_device\_create function in tvhdhomerun.c. This allows the function to handle ISDB type devices, which previously would have been changed to a DVB device on startup every time despite overrides.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/3ac184725c3d4b58aa6cd15691e6fab6a0d22e07) (2024-06-05)

***

## Release: [4.3-2324\~g543236118](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2324*) (2024-06-05)

> Docker/Alpine: Remove USB group
>
> The USB group has been removed from upstream alpine in commit bb00d0e4f345 ("main/alpine-baselayout: remove mem and usb group") which was a fixup on commit f16d0754d601 ("main/alpine-baselayout: remove unused/moved users and groups")
>
> Lets remove it here as well as we cannot join the group any longer.
>
> Besides, device access is probably better managed with host specific udev rules.
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/5432361184cc4afa585bf31914e58c0a0eee66ee) (2024-06-05)

***

## Release: [4.3-2322\~gc42043188](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2322*) (2024-04-26)

> Correct M3U playlist logo tag

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c42043188e73057cf9f5db0aefaed38f8384bbe8) (2024-04-26)

***

## Release: [4.3-2323\~g73a6bd00d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2323*) (2024-04-26)

> Fix echo target for superuser file in Debian postinst
>
> aba5e60792177d6a2a867445559f4806973b3258 was causing the username and password to get printed to the console instead of being put in the correct file. Also, use the modern $() syntax instead of \`\` and quote all variable assignments.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/73a6bd00d29421da04be5e1c41b2097fdc9c148b) (2024-04-26)

***

## Release: [4.3-2321\~gaba5e6079](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2321*) (2024-04-25)

> Properly escape json in setup

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/aba5e60792177d6a2a867445559f4806973b3258) (2024-04-25)

***

## Release: [4.3-2320\~gaaccc147e](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2320*) (2024-04-25)

> satip: Ignore additional parameters
>
> Instead or erroring, ignore additional parameters, as required by the specs in 3.5.11 where it says "Unknown attributes shall be ignored by the server"

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/aaccc147ea0aac385241d038fd7f1bd3f6d32d10) (2024-04-24)

***

## Release: [4.3-2319\~ga68d340a8](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2319*) (2024-04-21)

> configure: fix parsing args if values contain "="
>
> Currently, when the value of an option passed to the configure script as argument contains an equal sign "=", the part of the string up to the second equal sign is used as option. This commit changes how the string is split, so that always only the part up to the first equal sign is interpreted as option.
>
> "${var%=_}" removes everything from the last equal sign, "${var%%=_}" removes everything from the first equal sign.
>
> This allows to pass CFLAGS, which usually contain equal signs, like "--cflags=-march=armv6 -mfloat-abi=hard -mfpu=vfp"
>
> For reference: https://github.com/tvheadend/tvheadend/issues/1665
>
> Signed-off-by: MichaIng [micha@dietpi.com](mailto:micha@dietpi.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a68d340a89a3786c441185698ae999b86d77c777) (2024-04-20)

***

## Release: [4.3-2318\~gb10058507](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2318*) (2024-04-20)

> Update WebUI to allow debug/trace subsystem selection from a list.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b100585070ef794225397d7b99375a5bef246d46) (2024-04-20)

***

## Release: [4.3-2317\~g223f83b6e](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2317*) (2024-04-13)

> Add subsystems to JSON API.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/223f83b6ec616e5c254b97dd52bd49106b09e33a) (2024-04-13)

***

## Release: [4.3-2316\~g4874aaa31](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2316*) (2024-04-08)

> Fix detection of unknown version numbers in support/version
>
> Fixes: #1683

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/4874aaa3161fbdd8b9d3abe50fd3fa20b18f8b0b) (2024-04-08)

***

## Release: [4.3-2314\~gcbaf2b1de](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2314*) (2024-03-24)

> webui: Fix year being replaced incorrectly when using custom date format
>
> fixes regression in 2ca8a19

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/cbaf2b1de79206c311a3967cae5928e65c988daf) (2024-03-24)

***

## Release: [4.3-2315\~gab6ea89b1](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2315*) (2024-03-24)

> Update manpage
>
> * Replace freenode with libera
> * Change copyright info

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ab6ea89b11b1f1a8dcbfd7cfc29d65b3013f2702) (2024-03-24)

***

## Release: [4.3-2313\~gc63115464](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2313*) (2024-03-22)

> Translation for 'pl' updated. intl: Translate intl/docs/tvheadend.doc.pot in pl
>
> 100% translated source file: 'intl/docs/tvheadend.doc.pot' on 'pl'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c63115464d8f6556fb4cac93ce8740afea1b00d5) (2024-03-22)

***

## Release: [4.3-2312\~g19c502b15](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2312*) (2024-03-18)

> Translation for 'pl' updated. intl: Translate intl/docs/tvheadend.doc.pot in pl
>
> 98% of minimum 80% translated source file: 'intl/docs/tvheadend.doc.pot' on 'pl'.
>
> Sync of partially translated files: untranslated content is included with an empty translation or source language content depending on file format

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/19c502b15a91360470ca8212261acbe3f8f79058) (2024-03-18)

***

## Release: [4.3-2300\~g1212b940b](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2300*) (2024-03-14)

> Update README.md
>
> Existing (page not found) : https://cloudsmith.io/tvheadend/tvheadend
>
> New: https://cloudsmith.io/\~tvheadend/repos/tvheadend/packages/

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/1212b940b584e336da175361d02a5c193a3b65c0) (2024-03-14)

***

## Release: [4.3-2299\~g79aaa1434](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2299*) (2024-03-09)

> CI: remove NODIRTY option as those builds may be dirty

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/79aaa14346d9d40f3728c4b0fdc7b4240da76364) (2024-03-09)

***

## Release: [4.3-2298\~ge287b2fc6](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2298*) (2024-03-08)

> Revert accidental package renaming

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/e287b2fc600c9874e72211a97f2200d4e10ca574) (2024-03-08)

***

## Release: [4.3-2296\~gba3b5e56f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2296*) (2024-03-08)

> Create special tvheadend-armv6l and tvheadend-dbg-armv6l packages
>
> Fixes: #1665

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ba3b5e56f2f25efb8298a12b5118843de053813d) (2024-03-08)

***

## Release: [4.3-2295\~g4d5166ca4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2295*) (2024-03-07)

> Translation for 'pl' updated. intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/4d5166ca4b98299cff7a3d90e2fe44dc5720ad00) (2024-03-07)

***

## Release: [4.3-2292\~g9ac61d767](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2292*) (2024-03-03)

> update to libvpx 1.14.0-patch
>
> added patch

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/9ac61d7677feaf1078e2f3752cd8e580e2e61267) (2024-03-03)

***

## Release: [4.3-2290\~gae97d5bc5](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2290*) (2024-03-01)

> ci: added more info logging to cloudsmith.sh

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ae97d5bc57ae551febf342cca9b0c7c927a29d4d) (2024-03-01)

***

## Release: [4.3-2291\~ga9c6db8ac](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2291*) (2024-03-01)

> Improve autorec duplicate handling

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a9c6db8acbd85297238771b8b4430435b7994928) (2024-03-01)

***

## Release: [4.3-2289\~g7e694e3c0](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2289*) (2024-03-01)

> Translation for 'pl' updated. intl: Translate intl/js/tvheadend.js.pot in pl
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'pl'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7e694e3c0b45423769f914d1212e1f32336579ea) (2024-03-01)

***

## Release: [4.3-2286\~gae51d24fe](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2286*) (2024-02-24)

> Replace broken links, update copyright year

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ae51d24fe1c50a591d4e25ec76076560a6e2e962) (2024-02-23)

***

## Release: [4.3-2285\~g8b429efb7](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2285*) (2024-02-23)

> Translation for 'pl' updated. intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8b429efb72f6da7b62878bbb9ceafd14b8d00732) (2024-02-23)

***

## Release: [4.3-2268\~ga8f525f36](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2268*) (2024-02-22)

> Run enforce-pr-rebase whenever a PR is updated

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a8f525f36ca777345218726269ea2bb8ef1cbd43) (2024-02-21)

***

## Release: [4.3-2269\~g9b88c2502](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2269*) (2024-02-22)

> Translation for '(#1655)' updated. transifex: Updates for project Tvheadend and language pl (#1655)
>
> * intl: Translate intl/js/tvheadend.js.pot in pl
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'pl'.
>
> * intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * intl: Translate intl/js/tvheadend.js.pot in pl
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'pl'.
>
> * intl: Translate intl/js/tvheadend.js.pot in pl
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'pl'.
>
> * intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * intl: Translate intl/js/tvheadend.js.pot in pl
>
> 100% translated source file: 'intl/js/tvheadend.js.pot' on 'pl'.
>
> * intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> ***
>
> Co-authored-by: transifex-integration\[bot] <43880903+transifex-integration\[bot]@users.noreply.github.com>

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/9b88c25022f84c886232d60bc62bc6e6bfd47fb8) (2024-02-22)

***

## Release: [4.3-2271\~g7acca01c4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2271*) (2024-02-22)

> Give comment-on-labels.yml permissions to write to PRs

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7acca01c4153adc1dd409c82f27338fdeb353045) (2024-02-22)

***

## Release: [4.3-2270\~g60bd9dce6](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2270*) (2024-02-22)

> Add OpenCollective donate link to Wizard

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/60bd9dce6a10f80c09cc30b1be82825e0f1f805b) (2024-02-22)

***

## Release: [4.3-2266\~ge02e812ee](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2266*) (2024-02-21)

> Make sure we spawn the best matching executable and not the first match
>
> Fixes: #1632

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/e02e812ee550e93cd0aacaa9677036d977c1d94b) (2024-02-21)

***

## Release: [4.3-2258\~gc7a63e7e3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2258*) (2024-02-21)

> Replace poison memset by memset\_s to avoid compiler optimizing it out

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c7a63e7e3b7c15d6f2c1048efafbaaa5a854ea7d) (2024-02-20)

***

## Release: [4.3-2264\~gb8bd16726](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2264*) (2024-02-21)

> Translation for 'pl' updated. intl: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b8bd1672686f71ad5027a81e48e41eff8bfb11d8) (2024-02-20)

***

## Release: [4.3-2265\~g41a326bce](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2265*) (2024-02-21)

> ci: change CLOUDSMITH\_OWNER from a var to a secret

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/41a326bcecd80a2d4c6ca50b0e62af4acea894ba) (2024-02-21)

***

## Release: [4.3-2267\~g0d26809e3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2267*) (2024-02-21)

> Fix Auto-PR comment on squash-label

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0d26809e39c41bead3aef33fd4a815512aa312ab) (2024-02-21)

***

## Release: [4.3-2256\~gdf46dea35](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2256*) (2024-02-20)

> Add some ERRNOs for DVR & Config

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/df46dea3524b313bfeffa60dbeb42b4c93d44099) (2024-02-20)

***

## Release: [4.3-2254\~gc3a7ce11c](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2254*) (2024-02-20)

> Add missing tvheadend-prefix in JS file
>
> Fixes 2ca8a19e4c8761af1a6653fed09af658e9cd5b67

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c3a7ce11cec531f8eebaa9f9391e60379533cbe2) (2024-02-19)

***

## Release: [4.3-2257\~g771504eb3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2257*) (2024-02-20)

> Show SeriesLink for AutoRecs

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/771504eb3ea8540cc3c558e8fa91aa67acd6f350) (2024-02-20)

***

## Release: [4.3-2255\~g595bbaad5](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2255*) (2024-02-20)

> Shorten time for stale issues before a warning is applied

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/595bbaad56dba7c19eed54ced143d1c58c362c81) (2024-02-19)

***

## Release: [4.3-2252\~g4430ee70f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2252*) (2024-02-19)

> Add missing htmsg\_destroy() call in hdhomerun\_server\_discover

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/4430ee70f2a2888853d944fe7de619e51880f515) (2024-02-19)

***

## Release: [4.3-2253\~g2ca8a19e4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2253*) (2024-02-19)

> Add support for 12-hour custom date formats

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2ca8a19e4c8761af1a6653fed09af658e9cd5b67) (2024-02-19)

***

## Release: [4.3-2251\~g2b0b6a4c4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2251*) (2024-02-19)

> Replace single-bit signed integers with unsigned integers
>
> Single bit signed integers contain a single sign-byte and zero value bytes according to the C99 standard. This is not inteded here.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2b0b6a4c4c82adeaed9793f574e39247473c43e1) (2024-02-19)

***

## Release: [4.3-2229\~g6b5defc76](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2229*) (2024-02-12)

> CI: Ensure we clone the whole repo
>
> We have to make sure we clone the whole repo, so that `git describe` works as expected. Without it, we get version 0.0.0, not what we want.
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/6b5defc76d71c184a5a7a5e82f2a9c0eaf3a65f3) (2024-02-11)

***

## Release: [4.3-2228\~gce429efe9](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2228*) (2024-02-10)

> container: Add container support
>
> This commit adds support for containizersation of TVHeadend. It adds the actual technology agnostic container file, an entry point and healthcheck for it and a github workflow component to publish it.
>
> TODO: Healthcheck script is not yet working. TODO: Add decent documetnation
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ce429efe9bc48acd31cfb9f2e971fa3094a7f147) (2024-02-10)

***

## Release: [4.3-2227\~ga2ddd3066](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2227*) (2024-02-10)

> transcoding: access the codec name only when codec pointer is valid
>
> this fixes #1635

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a2ddd30661058955dd1ac3ff9e59b49dc4188bb6) (2024-02-09)

***

## Release: [4.3-2226\~gb91587037](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2226*) (2024-02-08)

> dvr: Fix incorrect usage of `strerror`
>
> `strerror` takes the `errno` directly as its argument, negating it will result in an "Unknown error".
>
> Signed-off-by: Tianyi Liu [i.pear@outlook.com](mailto:i.pear@outlook.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b91587037c6099e77d233877162e36138c62e5b2) (2024-02-08)

***

## Release: [4.3-2225\~g8bd13ca27](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2225*) (2024-02-07)

> Add "recordings" to the backup exclude list
>
> Since https://github.com/tvheadend/tvheadend/pull/1540, enabled by https://github.com/tvheadend/tvheadend/pull/1535 and https://github.com/tvheadend/tvheadend/pull/1538, we have been storing the recordings in a subdirectory of the configuration directory by default. Because of this, the recordings are getting stored in the configuration backup. This causes the backups to take forever and fill the disk (see https://github.com/tvheadend/tvheadend/issues/1625). Instead, exclude the "recordings" directory from the backup to prevent this.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8bd13ca278f3826826a0eeedf9ab1bce951b4244) (2024-02-07)

***

## Release: [4.3-2223\~g6409a6382](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2223*) (2024-02-06)

> descrambler: Fix Sky-UK descrambling

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/6409a6382f1ded18cd6f21649519879c410eb8ab) (2024-02-05)

***

## Release: [4.3-2224\~g63c41acc6](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2224*) (2024-02-06)

> Correct description of Change Parameters flag
>
> The Change Parameters flag on the Access Entries screen for a user determines whether that user's settings will override any previously-set parameters (for example from a wildcard user) - it does not affect the ability of subsequent users to override settings in turn. The exception is the 'Rights' settings where all matched users with the Change flag set are ORed together.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/63c41acc6ec404e202cf0e4f79cbbefd0daae895) (2024-02-06)

***

## Release: [4.3-2222\~g154cf25ad](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2222*) (2024-02-05)

> Translation for 'en\_US' updated. transifex: Translate tvheadend.js.pot in en\_US
>
> 100% translated source file: 'tvheadend.js.pot' on 'en\_US'.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/154cf25ada0da959e4ca3ab2353fcbf87bcec4cb) (2024-02-05)

***

## Release: [4.3-2213\~gf12919042](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2213*) (2024-02-04)

> Mark PRs needing squashing as stale after a while

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/f12919042c60566e3dd90d58940e3add60550e7a) (2024-02-03)

***

## Release: [4.3-2212\~gac4a041e0](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2212*) (2024-02-04)

> Automatically comment on PRs needing squash

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ac4a041e00529ba5325755061cd6caef0e3e8210) (2024-02-03)

***

## Release: [4.3-2215\~g9b00888e3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2215*) (2024-02-04)

> satipcli: Rename flag to include client reference
>
> We have both a satip client and server. However the nosatip flag, is for the client. Make this more clear by renaming it to the internal variable nosatipcli. Since we do not want to break the user facing API, we keep the commandline argument nosatip, but add an alias for the future.
>
> We can do better in the future with the rest of the satip reference, but lets keep this to a minimum for now.
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/9b00888e319c412a2a91008b1f78f4482975b879) (2024-02-04)

***

## Release: [4.3-2211\~g990b5a8f4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2211*) (2024-02-04)

> Fix audio-only timeshift memory usage

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/990b5a8f41dd9c0c039d4ce551e35809a4acbb22) (2024-02-03)

***

## Release: [4.3-2214\~g5acf42462](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2214*) (2024-02-04)

> Remove sweep-ai again as it is not useful at all

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/5acf42462141e26d2c5114c59b672c5f6cec634b) (2024-02-03)

***

## Release: [4.3-2210\~g154b20228](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2210*) (2024-02-03)

> Sanitize filename in content-disposition header

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/154b202288701013be926d5c13b205504483db93) (2024-02-03)

***

## Release: [4.3-2207\~gc7f46ec56](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2207*) (2024-02-02)

> Configure Sweep (#1612)
>
> Co-authored-by: sweep-ai\[bot] <128439645+sweep-ai\[bot]@users.noreply.github.com>

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c7f46ec5650ce7dda0b4f60bdb02b6996efff368) (2024-02-02)

***

## Release: [4.3-2209\~gb225e4d6c](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2209*) (2024-02-02)

> Clean up Debian postinst and postrm scripts
>
> * Fix indentation
> * Remove unnecessary {} around variables
> * Double-quote all variables when assigned or used as arguments
> * Simplify quotes and escaping in creation of the superuser file
> * Remove needless variable assignments
> * Use $() for command substitution instead of \`\`

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b225e4d6ccb966824f453aeabbd311799d24b471) (2024-02-02)

***

## Release: [4.3-2206\~g8ceb72f93](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2206*) (2024-02-02)

> Add stale-bot for issues/PRs needing more info

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8ceb72f9307371da3318ac2efea768a683548b2b) (2024-02-02)

***

## Release: [4.3-2205\~g0485cf470](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2205*) (2024-02-02)

> main: Warn about unexpected configuration location
>
> When using the `--fork` flag, and no user or config arguments are supplied, the configuration folder will end up with whatever the default `daemon` user has set, which is often `/sbin` set as the homedir.
>
> This is weird, but not 'wrong' per say. Lets warn the user that forking can have an unexpected side effect.
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0485cf470b64d3cfcc5a4e62c711789ff316cea8) (2024-02-02)

***

## Release: [4.3-2204\~g717056be0](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2204*) (2024-02-01)

> Use sigaction() instead of signal()
>
> The behavior of signal() is not consistent or defined when using it to set signal handlers (see "Portability" in https://man7.org/linux/man-pages/man2/signal.2.html). Previously we got away with this, but starting with GCC 14, using signal() apparently causes certain syscalls to be restarted after the signal is caught. One of these is the read() currently on line 63 of fsmonitor.c. The result is that read() doesn't return when the fsmonitor thread receives a signal, resulting in the thread never shutting down, resulting in TVHeadend hanging on any attempt to terminate it.
>
> Instead, use sigaction(), which has defined behavior when setting signal handlers. Since invoking sigaction() requires several lines, a helper was added to tvh\_thread.c to avoid code duplication.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/717056be02e1d1754bc86948c8523964c5ea0f1c) (2024-02-01)

***

## Release: [4.3-2203\~gbcfbe7dbe](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2203*) (2024-01-31)

> Add timeshift support for audio-only channels

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/bcfbe7dbeebb79c08fad22a214ecbfbbd426a3bd) (2024-01-31)

***

## Release: [4.3-2202\~gaf5e2c962](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2202*) (2024-01-31)

> templates: add log section to bug\_report.yml
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/af5e2c962a3ac7a170f343ef3beb9bdf18f34a93) (2024-01-31)

***

## Release: [4.3-2201\~g6229a74aa](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2201*) (2024-01-30)

> Add missing Lithuanian string template (#1608)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/6229a74aa08cc41fae2f64864543f961809531f1) (2024-01-30)

***

## Release: [4.3-2200\~g212e85c91](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2200*) (2024-01-28)

> ci: fix cloudsmith.sh & add to CI workflow

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/212e85c91e6138af58e9757fdb8893e1685d0cb5) (2024-01-28)

***

## Release: [4.3-2193\~gb7d5a1632](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2193*) (2024-01-21)

> update to ffmpeg 6.1.1
>
> update to ffmpeg 6.1.1

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b7d5a1632f3088368ade07bce7412f46968e9ae9) (2024-01-21)

***

## Release: [4.3-2192\~gc9b38a81a](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2192*) (2024-01-11)

> descrambler: apply ICAM update from Chris230291

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c9b38a81aa3d3a379d8b41cc0ffab1307304da48) (2024-01-11)

***

## Release: [4.3-2191\~gb4b1cbd47](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2191*) (2024-01-11)

> descrambler: avoid dlopen()

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b4b1cbd479f3ec3856ed35e5931eab2aff3892fd) (2024-01-11)

***

## Release: [4.3-2189\~g899b38ae5](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2189*) (2024-01-05)

> descrambler: support ICAM if detected in libdvbcsa

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/899b38ae5b960688b600be3e77526d92cecea536) (2024-01-04)

***

## Release: [4.3-2190\~g2151348f7](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2190*) (2024-01-05)

> linuxdvb: add DVB-S2X parameters

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2151348f7198061a22de3cfc4f4407634554003b) (2024-01-05)

***

## Release: [4.3-2188\~gb40a62b31](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2188*) (2024-01-01)

> ci: fix raspios detection in cloudsmith.sh
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b40a62b31e809523d2fe2f7f3f331cc55dfdbd0f) (2024-01-01)

***

## Release: [4.3-2187\~gfd8b9e8ba](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2187*) (2023-12-26)

> ci: rename build.yml to reduce confusion
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/fd8b9e8ba21600d0bf6cdb20a7cc153482a2efa5) (2023-12-26)

***

## Release: [4.3-2186\~g4825b8414](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2186*) (2023-12-18)

> Makefile.ffmpeg nvenc update
>
> FFNVCODEC\_VER = 11.1.5.0 -> 12.1.14.0

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/4825b8414fc276ee74e9d0c3ebf5eaf09825d6b6) (2023-12-18)

***

## Release: [4.3-2184\~g3cf5acdc7](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2184*) (2023-12-13)

> Remove references to Tvheadend Foundation.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/3cf5acdc714dc025b2246d2395478fcfd058afeb) (2023-12-13)

***

## Release: [4.3-2185\~g0da7fc0b7](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2185*) (2023-12-13)

> Transifex updates for project Tvheadend (#1587)
>
> * transifex: Translate tvheadend.js.pot in es
>
> 100% translated source file: 'tvheadend.js.pot' on 'es'.
>
> * transifex: Translate tvheadend.js.pot in en\_GB
>
> 100% translated source file: 'tvheadend.js.pot' on 'en\_GB'.
>
> * transifex: Translate tvheadend.js.pot in de
>
> 100% translated source file: 'tvheadend.js.pot' on 'de'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate intl/tvheadend.pot in pl
>
> 100% translated source file: 'intl/tvheadend.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> * transifex: Translate tvheadend.js.pot in pl
>
> 100% translated source file: 'tvheadend.js.pot' on 'pl'.
>
> ***
>
> Co-authored-by: transifex-integration\[bot] <43880903+transifex-integration\[bot]@users.noreply.github.com>

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/0da7fc0b7cf8f0159924d37a8c00b84ca3efdfc2) (2023-12-13)

***

## Release: [4.3-2183\~ga0bd2b359](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2183*) (2023-12-11)

> tfx: fix URLs in tvheadend/js files
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a0bd2b3590a2b059da37439d2445a35cfc796814) (2023-12-11)

***

## Release: [4.3-2171\~gf96ea6493](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2171*) (2023-12-06)

> ci: remove references to doozer
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/f96ea64930f4d2191f5df79e1331f28213805463) (2023-12-06)

***

## Release: [4.3-2175\~gd85c957aa](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2175*) (2023-12-06)

> WebUI: Update donation string as a test to Transifex feed

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/d85c957aa2b54c83301361f3d6dc7453def3302d) (2023-12-06)

***

## Release: [4.3-2173\~gb3ac61a01](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2173*) (2023-12-06)

> ci: schedule weekly coverity scans
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/b3ac61a01badb40320973cfcec978a97c56e6114) (2023-12-06)

***

## Release: [4.3-2172\~g8b34c31f2](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2172*) (2023-12-06)

> ci: add concurrency to the main CI workflows
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8b34c31f25078c985ac473c4843427c361372a2d) (2023-12-06)

***

## Release: [4.3-2174\~g49b095e18](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2174*) (2023-12-06)

> ci: remove the test-compile workflow
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/49b095e1850435d63c9c2f01f28770fdf46d55dd) (2023-12-06)

***

## Release: [4.3-2169\~g433cf8bbf](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2169*) (2023-12-06)

> ci: don't trigger cloudsmith on .github changes
>
> Signed-off-by: Christian Hewitt [christianshewitt@gmail.com](mailto:christianshewitt@gmail.com)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/433cf8bbf55b28b67c25defe2e81c186f11e4ea8) (2023-12-06)

***

## Release: [4.3-2166\~gae1ffbe57](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2166*) (2023-12-01)

> ci update build config

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ae1ffbe576742842c55ca3c685d829dd6df975f3) (2023-12-01)

***

## Release: [4.3-2167\~g583de2330](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2167*) (2023-12-01)

> gitignore: add debian/.debhelper folder

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/583de2330416e5122446920ef441c7e11129f92b) (2023-12-01)

***

## Release: [4.3-2162\~gbdadcb8b2](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2162*) (2023-11-28)

> Fix builds on stretch

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/bdadcb8b2bc07a65818a098b5db550bdbbf3caae) (2023-11-28)

***

## Release: [4.3-2161\~gbc30a74de](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2161*) (2023-11-21)

> Add rpi-bookworm to targets

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/bc30a74de8ab5efc3605afd68eb6d01d08170316) (2023-11-21)

***

## Release: [4.3-2160\~g2d963dab6](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2160*) (2023-11-20)

> Update ffmpeg to 5.1.4

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2d963dab6289028dd9f252dd41e13d881d6a9f92) (2023-11-20)

***

## Release: [4.3-2158\~g2d92f58fa](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2158*) (2023-10-15)

> 6310 Set 'okay' default to True

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/2d92f58fadf6b63c0a5a79a52d67f51e85b02be3) (2023-10-14)

***

## Release: [4.3-2157\~g3d16edb0f](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2157*) (2023-10-14)

> Removed nested function 'appendPidRange' from within function 'tvhdhomerun\_frontend\_update\_pids' and converted it to a normal function 'tvhdhomerun\_frontend\_update\_pids\_appendPidRange'.
>
> Nested functions are a non-standard extension to C that may only be supported by the gcc compiler.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/3d16edb0f59dd974b3924b463efc58be1cb1fac1) (2023-10-14)

***

## Release: [4.3-2154\~gec56067f4](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2154*) (2023-08-12)

> support/mkbundle: switch from distutils to setuptools
>
> Fixes build error with python-3.12:
>
> Traceback (most recent call last): File "support/mkbundle", line 48, in import distutils.spawn ModuleNotFoundError: No module named 'distutils'
>
> Signed-off-by: Bernd Kuhls [bernd@kuhls.net](mailto:bernd@kuhls.net)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/ec56067f4f6cb3fae5a03f0fb492c45413d095bb) (2023-08-11)

***

## Release: [4.3-2153\~g21911b5e3](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2153*) (2023-08-12)

> webui/dvr: Add age\_rating in recording details dialogs
>
> The details dialogs in the various recording tabs do not open anymore with the error `Uncaught TypeError: params[25] is undefined` in the JS console as the age\_rating wasn't requested for those, only for the overview columns.
>
> While we are at it lets also display the value in the same way the similar looking (but completely different implemented…) EPG dialog does.
>
> Regession-of: d501059995 Fixes: https://tvheadend.org/issues/6297

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/21911b5e37a20b6f2a10ef48a93ccf7bf2dd179c) (2023-08-11)

***

## Release: [4.3-2151\~g76ca76761](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2151*) (2023-08-09)

> Fix bug #6293 – Missing EIT EPG Content Type

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/76ca76761693eb7c1f347e79d271618f08ec3824) (2023-08-09)

***

## Release: [4.3-2149\~g17eebbef5](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2149*) (2023-08-06)

> otamux: Make sure we use PRItime\_t
>
> As %li isn't supported equally, we must ensure we always use PRItime\_t.
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/17eebbef5b017352afcded36c27cb0be11ebd4a1) (2023-08-06)

***

## Release: [4.3-2144\~gd50105999](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2144*) (2023-08-02)

> Add 'age rating' field to recording metadata

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/d50105999522cc7c35909f7c0f2a504fc40c2e1b) (2023-08-02)

***

## Release: [4.3-2143\~gfe47ecb55](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2143*) (2023-07-30)

> Fix time for 32bit systems again
>
> In issue #6257 an issue mentioning that time\_t isn't properly supported when printing on 32-bit systems, specifically on FreeBSD. However, intel 32-bit systems suffer from a similar fate:
>
> src/rtsp.c:333:30: error: format '%ld' expects argument of type 'long int', but argument 4 has type 'time\_t' {aka 'long long int'} \[-Werror=format=] 333 | snprintf(buf, sizeof(buf), "npt=%" PRItime\_t "-", position); | ^\~\~\~\~\~\~ \~\~\~\~\~\~\~\~ | | | time\_t {aka long long int}
>
> In commit 76a6263f1be4 ("fix for 64bit time\_t on 32bit systems") was attempted to be fixed by turning it into a PRId64, which was reverted again in commit 9e1eb89be731 ("Revert "fix for 64bit time\_t on 32bit systems""), sadly without a reason as to why in the commit message.
>
> We should however, migrate to 64bit timestamps on all platforms anyway, due to the Y2038 problem. Debian is heavily working on this issue too.
>
> This commit is just the first step, in that we ensure our time\_t is always 64bits.
>
> The next steps would be to use difftime where possible instead of subtractions, and ensure all stored timestamps have room for 64bit time\_t (htsmsg\_get\_u32\_or\_default for example breaks this presumption already).
>
> To keep this issue small, and tackle one problem at a time, lets just fix time\_t first. We do still have 15 years to fix the other issues.
>
> Note, that this patch leaves out FreeBSD specifics, as it is unclear what is specific about 32bit FreeBSD. It should be using the same glibc headers after all. If not, we can always add if needed, but adding usless code doesn't help anyone generally.
>
> ```
> diff --git a/src/tvheadend.h b/src/tvheadend.h
> index c2fcee716..751d10d70 100644
> --- a/src/tvheadend.h
> +++ b/src/tvheadend.h
> @@ -334,7 +334,9 @@ void tvh_qsort_r(void *base, size_t nmemb, size_t size, int (*compar)(const void
>  # endif /* ULONG_MAX */
>  #endif /* __WORDSIZE */
>
> -#if __WORDSIZE == 32
> +#if __WORDSIZE == 32 && defined(PLATFORM_FREEBSD)
> +# define PRItime_t "d"
> +#elif __WORDSIZE == 32
>  # define PRItime_t "lld"
>  #elif __WORDSIZE == 64
>  # define PRItime_t "ld"
>  #else
> ```
>
> Signed-off-by: Olliver Schinagl [oliver@schinagl.nl](mailto:oliver@schinagl.nl)

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/fe47ecb5504a521fed9c1ca9705fb0dd2bb8443a) (2023-07-30)

***

## Release: [4.3-2142\~g23263a54d](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2142*) (2023-07-30)

> OTA Genre translation squashed v2

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/23263a54d9bbda2779489c06d3aa909ec618ad63) (2023-07-30)

***

## Release: [4.3-2141\~gc531383ca](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2141*) (2023-07-19)

> Bug Fix: OTA EIT Parental Rating

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/c531383ca6654639dc112db67fd8dc893c1f5272) (2023-07-19)

***

## Release: [4.3-2139\~g7b5c52697](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2139*) (2023-06-23)

> Fix spelling errors encountered during previous work

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/7b5c526977eddfa4535df91ea4e23c8910c69b11) (2023-06-23)

***

## Release: [4.3-2118\~g8efac01dc](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2118*) (2023-04-17)

> update to ffmpeg 5.1.3
>
> update to ffmpeg 5.1.3

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/8efac01dccdf11b4b3b196080c085aaa801a62f7) (2023-04-17)

***

## Release: [4.3-2115\~ga10f7ea44](https://cloudsmith.io/~tvheadend/repos/tvheadend/packages/?q=version%3A4.3-2115*) (2023-04-02)

> tvhmeta: Fix tvhmeta authentication to the tvheadend API.
>
> Construct and add an Authorization header to the request, when a username and password are provided to tvhmeta.
>
> This fixes #6260.

> [GitHub commit details...](https://github.com/tvheadend/tvheadend/commit/a10f7ea4408e5ba2b0f04cc9db970873eafa883c) (2023-04-02)

***
