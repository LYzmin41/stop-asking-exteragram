# Stop Asking!

This ExteraGram plugin removes the extra **Voice Call**/**Video Call** confirmation sheet. Tapping either call button proceeds directly into ExteraGram's normal call flow.

The hook scans `VoIPHelper.startCall` overloads and changes the final `bypassConfirmation` argument only when the call has seven arguments and that final value is a boolean. ExteraGram has another seven-argument group-call overload whose final value is an account object, so it is left untouched. Permission checks, offline handling, account checks, unavailable-call handling, and call setup remain in ExteraGram.

There are no plugin settings.

## Install

Download `stop_asking.plugin`, import it through ExteraGram's plugin installer, enable **Stop Asking!**, and reopen the chat if the call menu was already open.

The source is `no_call_confirmation.py`. The `.plugin` file contains the same Python code with the extension required for catalog submission.

## Compatibility

- ExteraGram `12.9.0` or newer
- Plugin SDK `1.4.4.3` or newer

The hook was derived from the ExteraGram `12.9.0` APK and should be retested after an app update if the call implementation changes.
