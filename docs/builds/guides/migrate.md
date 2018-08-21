---
# Scope:
# * Introduction to the migration problem.
# * Underline that migrating is a complex and important task.
# * List and clarify the things that need attention when migrating.

category: builds-guides
order: 260
---

# Migration from CKEditor 4

When compared to its predecessor, CKEditor 5 should be considered **a totally new editor**. Every single aspect of it was redesigned &mdash; from installation, to integration, to features, to its data model, and finally to its API. Therefore, moving applications using a previous CKEditor version to version 5 cannot be simply called an "upgrade". It is something bigger, so the "migration" term fits better.

There is no "drop in" solution for migrating. In this guide we hope to summarize the most important aspects you need to consider before you proceed with installing CKEditor 5.

Before starting, be sure that migrating is your best choice. Refer to {@link builds/guides/overview#when-not-to-use-builds When NOT to use CKEditor 5 Builds?} for more information.

## Installation and integration

The very first aspect that changed with CKEditor 5 is its installation procedure. It became much more modern with the introduction of modular patterns, UMD, npm, etc. Refer to {@link builds/guides/integration/installation Installation} for more details.

The API for integrating CKEditor with your pages also changed. It is worth checking {@link builds/guides/integration/basic-api Basic API} for an introduction.

## Features

When it comes to features, there are two aspects that need to be taken into consideration:

* CKEditor 5 may still not have the same features available as CKEditor 4.
* Existing features may behave differently.

Therefore, it is worth spending some time analyzing required features.

CKEditor 5 was designed with focus on creating quality content. There are thus good reasons for it to not support some old features. You should take this chance to rethink the features available in your application and perhaps switch the approach towards a more modern reasoning.

## Image upload

Image upload is handled differently with CKEditor 5, bringing a much better user experience. Solutions used with CKEditor 4 may not be compatible anymore and therefore a new approach is needed.

CKEditor 5 Builds come with {@link features/image-upload#easy-image Easy Image} available out of the box. It is super simple to {@link features/image-upload#easy-image enable image upload with it}.

## Plugins

The trickiest migration challenge to be faced may be related to custom plugins you have developed for CKEditor 4. Although their concept may stay the same, their implementation will certainly be different and will require rewriting them from scratch.

The same may apply for third-party plugins which may not have been ported to CKEditor 5 yet.

Check the {@link builds/guides/development/plugins#creating-plugins Creating plugins} section for more information on the development of plugins.

## Themes (skins)

In CKEditor 5, the previous concept of "skins" was reviewed and is now called "themes".

If you have custom skins for CKEditor 4, these skins need to be recreated for CKEditor 5. Fortunately, {@link framework/guides/theme-customization custom theming} in CKEditor 5 is much more powerful and simpler than before.

<!--
For more information, check how to {@linkTODO create new themes in the CKEditor 5 Framework documentation}.
-->

## Existing data

An extremely important aspect to be remembered is that &mdash; because of the difference in features &mdash; the **data produced with CKEditor 4 may not be compatible with CKEditor 5 (which may lead to data loss)**.

Extensive analysis, data verification and tests should be performed on existing data. If necessary, you will need to develop conversion procedures to avoid data loss. A relatively simple yet efficient strategy of adopting CKEditor 5 into existing systems might be using CKEditor 5 for creating new content and the old editor for editing legacy content.

## Configuration options compatibility table


The following table presents configuration options available in CKEditor 4 and their equivalent in CKEditor 5.

Note: The number of options was reduced on purpose. We understood that configuring CKEditor 4 was a bit too troublesome due to the number of configuration options available (over 240). Sometimes they were definitely too low-level, also many times they were so infrequently used that it did not justify the increased level of the application complexity. This is why when designing CKEditor 5 from scratch, we decided to come with a simplified editor, with well-thought default behavior, based on the results of the [Editor Recommendations](http://ckeditor.github.io/editor-recommendations/) project.

<table class="docsearch-txt">
	<thead>
		<tr>
			<th>CKEditor 4</th>
			<th>CKEditor 5</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span id="allowedContent"><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-allowedContent">allowedContent</a></span></td>
			<td>
				<p>Extending the list of HTML tags or attributes that CKEditor should support can be achieved by writing a plugin that (ideally) provides also means to control (insert, edit, delete) such markup.</p>
				<p>For more information on how to create plugins check the {@link framework/guides/quick-start#creating-a-simple-plugin Creating a simple plugin} article. Looking at the source code of CKEditor 5 plugins may also give you a lot of inspiration.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoEmbed_widget">autoEmbed_widget</a></td>
			<td>Media embedding is not supported yet, but it is planned.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoGrow_bottomSpace">autoGrow_bottomSpace</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoGrow_maxHeight">autoGrow_maxHeight</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoGrow_minHeight">autoGrow_minHeight</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoGrow_onStartup">autoGrow_onStartup</a></td>
			<td>
				<p>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, which means that the height (and similar options) of the editing area can be easily controlled with CSS. For example the <code>minHeight</code> and <code>maxHeight</code> settings can be achieved with <code>.ck-content { min-height:200px; max-height:400px; }</code>.</p>
				<p> See also <a href="https://stackoverflow.com/questions/46559354/how-to-set-the-height-of-ckeditor-5-classic-editor" target="_blank" rel="noopener">How to set the height of CKEditor 5 (Classic editor)</a>.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-autoUpdateElement">autoUpdateElement</a></td>
			<td>CKEditor 5 always updates the replaced element. This behavior cannot be disabled.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-baseFloatZIndex">baseFloatZIndex</a></td>
			<td>N/A. There is a dedicated <a href="https://github.com/ckeditor/ckeditor5-ui/issues/218" target="_blank" rel="noopener">issue about z-index management</a> and making it more open for developers.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-baseHref">baseHref</a></td>
			<td>Not supported yet, see <a href="https://github.com/ckeditor/ckeditor5/issues/665" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5/issues/665</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-basicEntities">basicEntities</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-blockedKeystrokes">blockedKeystrokes</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-bodyClass">bodyClass</a></td>
			<td>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, so such setting is no longer needed. Simply wrap the editor with a <code>&lt;div class=&quot;...&quot;&gt;</code> to achieve a similar result. When using {@link examples/builds/balloon-editor Balloon} or {@link examples/builds/inline-editor Inline} editor you may add a class to the element on which the editor is initialized.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-bodyId">bodyId</a></td>
			<td>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, so such setting is no longer needed. Simply wrap the editor with a <code>&lt;div id=&quot;...&quot;&gt;</code> to achieve a similar result. When using Balloon or Inline editor you may add a class to the element on which the editor is initialized.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-browserContextMenuOnCtrl">browserContextMenuOnCtrl</a></td>
			<td>No longer needed as CKEditor 5 does not have its own context menu and does not block the native browser context menu.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-clipboard_defaultContentType">clipboard_defaultContentType</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-clipboard_notificationDuration">clipboard_notificationDuration</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-codeSnippetGeshi_url">codeSnippetGeshi_url</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-codeSnippet_codeClass">codeSnippet_codeClass</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-codeSnippet_languages">codeSnippet_languages</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-codeSnippet_theme">codeSnippet_theme</a></td>
			<td>
				<p>Code blocks are not supported yet. A plugin adding support for the inline <code>&lt;code&gt;</code> element is already included in the {@link features/basic-styles Basic styles} package.</p>
				<p>Note: The {@link module:basic-styles/code~Code Code feature} is not available by default in any build, but can be enabled in a {@link builds/guides/development/custom-builds custom build}.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_backStyle">colorButton_backStyle</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_colors">colorButton_colors</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_colorsPerRow">colorButton_colorsPerRow</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_enableAutomatic">colorButton_enableAutomatic</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_enableMore">colorButton_enableMore</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_foreStyle">colorButton_foreStyle</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-colorButton_normalizeBackground">colorButton_normalizeBackground</a></td>
			<td>
				<p>The &#x201C;classic&#x201D; font/background color feature will be provided in the future.</p>
				<p>At the same time, we already provide a new Highlight plugin which allows for highlighting parts of the text with the <code>&lt;mark&gt;</code> element with different CSS classes that can be easily styled. See the {@link features/highlight Highlight feature guide} for more information .</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-contentsCss">contentsCss</a></td>
			<td>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, so such file and configuration setting is no longer needed. If for some reason you need to style the contents of the editing area differently, use the <code>.ck-content</code> selector.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-contentsLangDirection">contentsLangDirection</a></td>
			<td>In case of Inline or Balloon editor, just add the <code>dir</code> attribute to the edited element. In case of Classic editor, see <a href="https://github.com/ckeditor/ckeditor5/issues/671" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5/issues/671</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-contentsLanguage">contentsLanguage</a></td>
			<td>In case of Inline or Balloon editor, just add the <code>lang</code> attribute to the edited element. In case of Classic editor, see <a href="https://github.com/ckeditor/ckeditor5/issues/670" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5/issues/670</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_allowRules">copyFormatting_allowRules</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_allowedContexts">copyFormatting_allowedContexts</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_disallowRules">copyFormatting_disallowRules</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_keystrokeCopy">copyFormatting_keystrokeCopy</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_keystrokePaste">copyFormatting_keystrokePaste</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-copyFormatting_outerCursor">copyFormatting_outerCursor</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_bold">coreStyles_bold</a></td>
			<td>CKEditor 5 uses the <code>&lt;strong&gt;</code> element, see <a href="https://ckeditor.github.io/editor-recommendations/features/bold.html" target="_blank" rel="noopener">Editor Recommendations - Bold</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_italic">coreStyles_italic</a></td>
			<td>CKEditor 5 uses the <code>&lt;i&gt;</code> element, see <a href="https://ckeditor.github.io/editor-recommendations/features/italic.html" target="_blank" rel="noopener">Editor Recommendations - Italic</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_strike">coreStyles_strike</a></td>
			<td>CKEditor 5 uses the <code>&lt;s&gt;</code> element, see <a href="https://ckeditor.github.io/editor-recommendations/features/strikethrough.html" target="_blank" rel="noopener">Editor Recommendations - Strikethrough</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_subscript">coreStyles_subscript</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_superscript">coreStyles_superscript</a></td>
			<td>Planned.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-coreStyles_underline">coreStyles_underline</a></td>
			<td>
				<p>CKEditor 5 uses the <code>&lt;u&gt;</code> element, see <a href="https://github.com/ckeditor/editor-recommendations/issues/4" target="_blank" rel="noopener">Editor Recommendations - Underline</a>.</p>
				<p>Note: The {@link module:basic-styles/underline~Underline Underline feature} is not available by default in any build, but can be enabled in a {@link builds/guides/development/custom-builds custom build} (see the {@link features/basic-styles Basic styles} feature guide).</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-customConfig">customConfig</a></td>
			<td>For performance reasons, CKEditor 5 no longer loads a separate configuration file. Passing configuration options inline reduces the number of HTTP requests.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dataIndentationChars">dataIndentationChars</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><span id="defaultLanguage"><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-defaultLanguage">defaultLanguage</a></span></td>
			<td>The support for multiple translations is handled by the translations service. See {@link features/ui-language}</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-devtools_styles">devtools_styles</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-devtools_textCallback">devtools_textCallback</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_backgroundCoverColor">dialog_backgroundCoverColor</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_backgroundCoverOpacity">dialog_backgroundCoverOpacity</a></td>
			<td>The use of configuration options to style selected parts of the editor was dropped in favor of much more powerful {@link framework/guides/theme-customization theme customization}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_buttonsOrder">dialog_buttonsOrder</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_magnetDistance">dialog_magnetDistance</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_noConfirmCancel">dialog_noConfirmCancel</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-dialog_startupFocusTab">dialog_startupFocusTab</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-disableNativeSpellChecker">disableNativeSpellChecker</a></td>
			<td>
				<p>Unavailable, however, in case of Inline and Balloon editors can be done by setting the <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/spellcheck" target="_blank" rel="noopener"><code>spellcheck</code></a> attribute directly on the element where CKEditor should be enabled.</p>
				<p>For Classic editor, call <code>editor.ui.view.editable.editableElement.setAttribute(&apos;spellcheck&apos;, &apos;false&apos;);</code> after creating the editor.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-disableNativeTableHandles">disableNativeTableHandles</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-disableObjectResizing">disableObjectResizing</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-disableReadonlyStyling">disableReadonlyStyling</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-disallowedContent">disallowedContent</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-div_wrapTable">div_wrapTable</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-docType">docType</a></td>
			<td>N/A. CKEditor 5 no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, so the editor is using the same doctype as the page where it operates.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-emailProtection">emailProtection</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-embed_provider">embed_provider</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-enableContextMenu">enableContextMenu</a></td>
			<td>N/A. CKEditor 5 does not come with a context menu, contextual inline toolbar is preferred instead to offer contextual actions.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-enableTabKeyTools">enableTabKeyTools</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><span id="enterMode"><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-enterMode">enterMode</a></span></td>
			<td>N/A. CKEditor 5 always creates a new paragraph (<code>&lt;p&gt;</code> element) as specified by <a href="http://ckeditor.github.io/editor-recommendations/usability/enter-key.html" target="_blank" rel="noopener">Editor Recommendations - Enter key</a>. <kbd>Shift</kbd> + <kbd>Enter</kbd> support is handled in <a href="https://github.com/ckeditor/ckeditor5-enter/issues/2" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5-enter/issues/2</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-entities">entities</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-entities_additional">entities_additional</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-entities_greek">entities_greek</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-entities_latin">entities_latin</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-entities_processNumerical">entities_processNumerical</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-extraAllowedContent">extraAllowedContent</a></td>
			<td>See <a href="#allowedContent"><code>config.allowedContent</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-extraPlugins">extraPlugins</a></td>
			<td>Enabling extra plugins is possible by creating a {@link builds/guides/development/custom-builds custom build}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fileTools_defaultFileName">fileTools_defaultFileName</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserBrowseUrl">filebrowserBrowseUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserFlashBrowseUrl">filebrowserFlashBrowseUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserFlashUploadUrl">filebrowserFlashUploadUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserImageBrowseLinkUrl">filebrowserImageBrowseLinkUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserImageBrowseUrl">filebrowserImageBrowseUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserImageUploadUrl">filebrowserImageUploadUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserUploadUrl">filebrowserUploadUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserWindowFeatures">filebrowserWindowFeatures</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserWindowHeight">filebrowserWindowHeight</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-filebrowserWindowWidth">filebrowserWindowWidth</a></td>
			<td>There is no equivalent of the file browser plugin in CKEditor 5 yet. See also <a href="#uploadUrl"><code>config.uploadUrl</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fillEmptyBlocks">fillEmptyBlocks</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-find_highlight">find_highlight</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-flashAddEmbedTag">flashAddEmbedTag</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-flashConvertOnEdit">flashConvertOnEdit</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-flashEmbedTagOnly">flashEmbedTagOnly</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-floatSpaceDockedOffsetX">floatSpaceDockedOffsetX</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-floatSpaceDockedOffsetY">floatSpaceDockedOffsetY</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-floatSpacePinnedOffsetX">floatSpacePinnedOffsetX</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-floatSpacePinnedOffsetY">floatSpacePinnedOffsetY</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-floatSpacePreferRight">floatSpacePreferRight</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fontSize_defaultLabel">fontSize_defaultLabel</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fontSize_sizes">fontSize_sizes</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fontSize_style">fontSize_style</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-font_defaultLabel">font_defaultLabel</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-font_names">font_names</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-font_style">font_style</a></td>
			<td>See the {@link features/font Font feature} guide.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-forceEnterMode">forceEnterMode</a></td>
			<td>N/A. Se also <a href="#enterMode"><code>config.enterMode</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-forcePasteAsPlainText">forcePasteAsPlainText</a></td>
			<td>N/A. No longer needed as CKEditor 5 removes all unwanted markup that cannot be edited with the editor.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-forceSimpleAmpersand">forceSimpleAmpersand</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_address">format_address</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_div">format_div</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_p">format_p</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_pre">format_pre</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h1">format_h1</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h2">format_h2</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h3">format_h3</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h4">format_h4</a> <br>  <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h5">format_h5</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_h6">format_h6</a></td>
			<td>All headings are configurable via {@link module:heading/heading~HeadingConfig#options <code>heading.options</code>}. See also the {@link features/headings Headings feature guide}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-format_tags">format_tags</a></td>
			<td>N/A. In order to enable additional block tags in CKEditor 5 a dedicated plugin must be provided. See also <a href="#allowedContent"><code>config.allowedContent</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-fullPage">fullPage</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-grayt_autoStartup">grayt_autoStartup</a></td>
			<td>N/A. There is no grammar checking plugin in CKEditor 5 at this moment. However, the native browser spell checker can be used in CKEditor 5.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-height">height</a></td>
			<td>
				<p>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, which means that the height (and similar options) of the editing area can be easily controlled with CSS. For example the height setting can be achieved with <code>.ck-content { height:400px; }</code>.</p>
				<p>See also <a href="https://stackoverflow.com/questions/46559354/how-to-set-the-height-of-ckeditor-5-classic-editor" target="_blank" rel="noopener">How to set the height of CKEditor 5 (Classic editor)</a>.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-htmlEncodeOutput">htmlEncodeOutput</a></td>
			<td>N/A. CKEditor 5 outputs HTML markup. See also <a href="https://stackoverflow.com/questions/47555667/ckeditor-5-htmlencodeoutput-doesnt-work" target="_blank" rel="noopener">https://stackoverflow.com/questions/47555667/ckeditor-5-htmlencodeoutput-doesnt-work</a> and a <a href="https://github.com/ckeditor/ckeditor5/issues/698" target="_blank" rel="noopener">dedicated issue</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-ignoreEmptyParagraph">ignoreEmptyParagraph</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image2_alignClasses">image2_alignClasses</a></td>
			<td>Available via more powerful {@link module:image/image~ImageConfig#styles <code>image.styles</code>}. This also allows for using custom style definitions, not only left, right and center alignment. See the <a href="https://ckeditor.com/docs/ckeditor5/latest/features/image.html#image-styles" target="_blank" rel="noopener">Image styles feature overview</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image2_altRequired">image2_altRequired</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image2_captionedClass">image2_captionedClass</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image2_disableResizer">image2_disableResizer</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image2_prefillDimensions">image2_prefillDimensions</a>.</td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-imageUploadUrl">imageUploadUrl</a></td>
			<td>See <a href="#uploadUrl"><code>config.uploadUrl</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image_prefillDimensions">image_prefillDimensions</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image_previewText">image_previewText</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-image_removeLinkByEmptyURL">image_removeLinkByEmptyURL</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-indentClasses">indentClasses</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-indentOffset">indentOffset</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-indentUnit">indentUnit</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-jqueryOverrideVal">jqueryOverrideVal</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-justifyClasses">justifyClasses</a></td>
			<td>See {@link features/text-alignment text alignment feature guide}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-keystrokes">keystrokes</a></td>
			<td>
				<p>Keystroke handlers can be registered using {@link module:core/editingkeystrokehandler~EditingKeystrokeHandler <code>EditingKeystrokeHandler</code>}. More information and examples can be found in a dedicated {@link framework/guides/architecture/intro#keystroke-handler Keystrokes and focus management} article.</p>
				<p>Making keystrokes overridable through <code>config.keystrokes</code> is handled in a <a href="https://github.com/ckeditor/ckeditor5-core/issues/8" target="_blank" rel="noopener">dedicated issue</a>. There is also an issue about <a href="https://github.com/ckeditor/ckeditor5-core/issues/20" target="_blank" rel="noopener">improving keystroke handling</a>.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-language">language</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-language_list">language_list</a></td>
			<td>See <a href="#defaultLanguage"><code>config.uploadUrl</code></a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-linkJavaScriptLinksAllowed">linkJavaScriptLinksAllowed</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-linkShowAdvancedTab">linkShowAdvancedTab</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-linkShowTargetTab">linkShowTargetTab</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_color">magicline_color</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_everywhere">magicline_everywhere</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_holdDistance">magicline_holdDistance</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_keystrokeNext">magicline_keystrokeNext</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_keystrokePrevious">magicline_keystrokePrevious</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_tabuList">magicline_tabuList</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-magicline_triggerOffset">magicline_triggerOffset</a></td>
			<td>N/A. The magic line feature itself is planned.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-mathJaxClass">mathJaxClass</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-mathJaxLib">mathJaxLib</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-menu_groups">menu_groups</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-menu_subMenuDelay">menu_subMenuDelay</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-newpage_html">newpage_html</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-notification_duration">notification_duration</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-on">on</a></td>
			<td>
				<p>Using the configuration file or setting to define event listeners was a bad practice so support for it was dropped.</p>
				<p>When creating an editor, a <code>Promise</code> is returned. Use <code>then/catch()</code> to define a callback when the editor is initialized or fails to start. The promise returns the created editor instance, e.g. {@link module:editor-classic/classiceditor~ClassicEditor <code>ClassicEditor</code>}, on which you can listen to its events.</p>
				<p>Note: The editor instance is not the only object on which events are fired. You can also listen to e.g. {@link module:engine/model/document~Document `Document`} events.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-pasteFilter">pasteFilter</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-pasteFromWordCleanupFile">pasteFromWordCleanupFile</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-pasteFromWordPromptCleanup">pasteFromWordPromptCleanup</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-pasteFromWord_heuristicsEdgeList">pasteFromWord_heuristicsEdgeList</a></td>
			<td>N/A. The Paste from Word feature itself is planned.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-plugins">plugins</a></td>
			<td>See the {@link module:core/editor/editorconfig~EditorConfig#plugins <code>plugins</code>} configuration option. The way how plugins are enabled in CKEditor 5 has changed in general. For more information check the articles about {@link builds/guides/development/plugins plugins} and {@link builds/guides/development/custom-builds custom builds}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-protectedSource">protectedSource</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-readOnly">readOnly</a></td>
			<td>See {@link module:core/editor/editor~Editor#isReadOnly <code>editor.isReadOnly</code>} and {@link features/read-only Read-only feature guide}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-removeButtons">removeButtons</a></td>
			<td>N/A. A similar effect can be achieved by setting the {@link module:core/editor/editorconfig~EditorConfig#toolbar <code>toolbar</code>} option with fewer buttons.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-removeDialogTabs">removeDialogTabs</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-removeFormatAttributes">removeFormatAttributes</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-removeFormatTags">removeFormatTags</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-removePlugins">removePlugins</a></td>
			<td>{@link module:core/editor/editorconfig~EditorConfig#removePlugins <code>removePlugins</code>}</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_dir">resize_dir</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_enabled">resize_enabled</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_maxHeight">resize_maxHeight</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_maxWidth">resize_maxWidth</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_minHeight">resize_minHeight</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-resize_minWidth">resize_minWidth</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_autoStartup">scayt_autoStartup</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_contextCommands">scayt_contextCommands</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_contextMenuItemsOrder">scayt_contextMenuItemsOrder</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_customDictionaryIds">scayt_customDictionaryIds</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_customPunctuation">scayt_customPunctuation</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_customerId">scayt_customerId</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_disableOptionsStorage">scayt_disableOptionsStorage</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_elementsToIgnore">scayt_elementsToIgnore</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_handleCheckDirty">scayt_handleCheckDirty</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_handleUndoRedo">scayt_handleUndoRedo</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_ignoreAllCapsWords">scayt_ignoreAllCapsWords</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_ignoreDomainNames">scayt_ignoreDomainNames</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_ignoreWordsWithMixedCases">scayt_ignoreWordsWithMixedCases</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_ignoreWordsWithNumbers">scayt_ignoreWordsWithNumbers</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_inlineModeImmediateMarkup">scayt_inlineModeImmediateMarkup</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_maxSuggestions">scayt_maxSuggestions</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_minWordLength">scayt_minWordLength</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_moreSuggestions">scayt_moreSuggestions</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_multiLanguageMode">scayt_multiLanguageMode</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_multiLanguageStyles">scayt_multiLanguageStyles</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_sLang">scayt_sLang</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_serviceHost">scayt_serviceHost</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_servicePath">scayt_servicePath</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_servicePort">scayt_servicePort</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_serviceProtocol">scayt_serviceProtocol</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_srcUrl">scayt_srcUrl</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_uiTabs">scayt_uiTabs</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-scayt_userDictionaryName">scayt_userDictionaryName</a></td>
			<td>N/A. There is no spell checking plugin in CKEditor 5 at this moment. However, the native browser spell checker can be used in CKEditor 5.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-sharedSpaces">sharedSpaces</a></td>
			<td>N/A. CKEditor 5 Framework architecture allows for writing a custom editor that contains multiple editable elements (document roots). See the {@link framework/guides/document-editor Document editor tutorial}.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-shiftEnterMode">shiftEnterMode</a></td>
			<td>N/A. <kbd>Shift</kbd> + <kbd>Enter</kbd> support is handled in <a href="https://github.com/ckeditor/ckeditor5-enter/issues/2" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5-enter/issues/2</a></td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-skin">skin</a></td>
			<td>
				<p>In CKEditor 5 lots of changes to the interface can be easily made by changing the default CKEditor theme (see the {@link examples/theme-customization Theme customization guide}).</p>
				<p>For heavy UI modifications, like integrating CKEditor with a custom UI framework, building a custom editor is needed (see the {@link examples/theme-customization Third-party UI guide}).</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-smiley_columns">smiley_columns</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-smiley_descriptions">smiley_descriptions</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-smiley_images">smiley_images</a> <br>  <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-smiley_path">smiley_path</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-sourceAreaTabSize">sourceAreaTabSize</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-specialChars">specialChars</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-startupFocus">startupFocus</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-startupMode">startupMode</a></td>
			<td>N/A. View source feature is not planned, see <a href="https://github.com/ckeditor/ckeditor5/issues/592" target="_blank" rel="noopener">https://github.com/ckeditor/ckeditor5/issues/592</a>.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-startupOutlineBlocks">startupOutlineBlocks</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-startupShowBorders">startupShowBorders</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-stylesSet">stylesSet</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-stylesheetParser_skipSelectors">stylesheetParser_skipSelectors</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-stylesheetParser_validSelectors">stylesheetParser_validSelectors</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-tabIndex">tabIndex</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-tabSpaces">tabSpaces</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-templates">templates</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-templates_files">templates_files</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-templates_replaceContent">templates_replaceContent</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-title">title</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbar">toolbar</a></td>
			<td>
				<p>{@link module:core/editor/editorconfig~EditorConfig#toolbar <code>toolbar</code>}</p>
				<p>See also {@link module:core/editor/editorconfig~EditorConfig#balloonToolbar <code>contextualToolbar</code>} to define the toolbar of a Balloon editor.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbarCanCollapse">toolbarCanCollapse</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbarGroupCycling">toolbarGroupCycling</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbarGroups">toolbarGroups</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbarLocation">toolbarLocation</a></td>
			<td>N/A. Can be achieved by writing an editor with a customized UI view. See also the {@link module:editor-decoupled/decouplededitor~DecoupledEditor <code>DecoupledEditor</code>} implementation.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-toolbarStartupExpanded">toolbarStartupExpanded</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-uiColor">uiColor</a></td>
			<td>CKEditor 5 comes with a concept of much more powerful themes, where almost every aspect of the UI can be styled easily. See the {@link framework/guides/theme-customization Theme customization guide} and {@link examples/theme-customization Theme customization guide}. Thanks to {@link framework/guides/theme-customization#customization-with-css-variables CSS variables} rebuilding the editor is not needed to change its styles.</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-undoStackSize">undoStackSize</a></td>
			<td>{@link module:typing/typing~TypingConfig#undoStep <code>typing.undoStep</code>}</td>
		</tr>
		<tr>
			<td><span id="uploadUrl"><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-uploadUrl">uploadUrl</a></span></td>
			<td>
				<p>Uploading images in CKEditor 5 is possible thanks to {@link features/image-upload#easy-image Easy Image} powered by <a href="https://ckeditor.com/ckeditor-cloud-services/" target="_blank" rel="noopener">CKEditor Cloud Services</a> which comes with support for responsive images. To configure it, provide the {@link module:cloud-services/cloudservices~CloudServicesConfig cloud services configuration}. Uploading via CKFinder is available, too, see {@link module:adapter-ckfinder/uploadadapter~CKFinderAdapterConfig#uploadUrl <code>ckfinder.uploadUrl</code>}. </p>
				<p>Writing your own image upload adapters is also possible, see <a href="https://stackoverflow.com/questions/46765197/how-to-enable-image-upload-support-in-ckeditor-5" target="_blank" rel="noopener">https://stackoverflow.com/questions/46765197/how-to-enable-image-upload-support-in-ckeditor-5</a>.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-useComputedState">useComputedState</a></td>
			<td>N/A</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-width">width</a></td>
			<td>
				<p>Classic editor (CKEditor 5) no longer encapsulates the editing area in an <code>&lt;iframe&gt;</code>, which means that the height (and similar options) of the editing area can be easily controlled with CSS. For example, the width setting can be achieved with <code>.ck-content { width:400px; }</code>.</p>
				<p>See also <a href="https://stackoverflow.com/questions/46559354/how-to-set-the-height-of-ckeditor-5-classic-editor" target="_blank" rel="noopener">How to set the height of CKEditor 5 (Classic editor)</a>.</p>
			</td>
		</tr>
		<tr>
			<td><a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_cmd">wsc_cmd</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_customDictionaryIds">wsc_customDictionaryIds</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_customLoaderScript">wsc_customLoaderScript</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_customerId">wsc_customerId</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_height">wsc_height</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_lang">wsc_lang</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_left">wsc_left</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_top">wsc_top</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_userDictionaryName">wsc_userDictionaryName</a> <br> <a href="/ckeditor4/docs/#!/api/CKEDITOR.config-cfg-wsc_width">wsc_width</a></td>
			<td>There is no spell checking plugin in CKEditor 5 at this moment. However, the native browser spell checker can be used in CKEditor 5.</td>
		</tr>
	</tbody>
</table>

If you are missing any particular features or settings, feel free to {@link builds/guides/support/reporting-issues#reporting-issues-2 report an issue}. Please be as precise as possible, explaining the exact use case, the context where the editor is used, and the expected behavior.
