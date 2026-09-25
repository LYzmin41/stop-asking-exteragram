"""Start Telegram audio and video calls without the extra confirmation dialog."""

from base_plugin import BasePlugin, MethodHook
from hook_utils import find_class


__id__ = "no_call_confirmation"
__name__ = "Stop Asking!"
__description__ = "Starts audio and video calls immediately without the confirmation dialog."
__author__ = "LYzmin41"
__version__ = "1.0.1"
__app_version__ = ">=12.9.0"
__sdk_version__ = ">=1.4.4.3"


class _StartCallHook(MethodHook):
    """Mark only the user-call overload as already confirmed."""

    def __init__(self, plugin):
        self.plugin = plugin

    def before_hooked_method(self, param):
        args = param.args
        if args is None or len(args) != 7:
            return

        # VoIPHelper has one seven-argument group-call overload whose final
        # argument is AccountInstance. The user-call overload ends in the
        # primitive bypassConfirmation boolean.
        if not isinstance(args[6], bool):
            return

        args[6] = True
        self.plugin.log("No Call Confirmation: bypass flag applied")


class NoCallConfirmation(BasePlugin):
    """Remove only the confirmation step; Telegram keeps the call flow."""

    def on_plugin_load(self):
        try:
            voip_helper = find_class("org.telegram.ui.Components.voip.VoIPHelper")
            # The SDK's class wrapper does not expose Java reflection methods
            # directly. hook_all_methods resolves the overloads for us.
            self.hooks = self.hook_all_methods(
                voip_helper,
                "startCall",
                _StartCallHook(self),
            )
            self.log(
                "No Call Confirmation: hook installed "
                f"count={len(self.hooks) if self.hooks else 0}"
            )
        except Exception as exc:
            self.log(f"No Call Confirmation: hook installation failed: {exc}")
