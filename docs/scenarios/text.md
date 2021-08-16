---
title:Working with Plain Text Requests
editLink:true
---

If you find yourself needing to test HTTP endpoints that either send text or return text, Alba
has you covered with some built in helpers.

## Reading the Response Text

To read the response body as text, use this syntax:

<!-- snippet: sample_read_text -->
<a id='snippet-sample_read_text'></a>
```cs
public async Task read_text(IAlbaHost system)
{
    var result = await system.Scenario(_ =>
    {
        _.Get.Url("/output");
    });

    // This deserializes the response body to the
    // designated Output type
    var outputString = result.ReadAsText();

    // do assertions against the Output string
}
```
<sup><a href='https://github.com/JasperFx/alba/blob/master/src/Alba.Testing/Samples/JsonAndXml.cs#L65-L79' title='Snippet source file'>snippet source</a> | <a href='#snippet-sample_read_text' title='Start of snippet'>anchor</a></sup>
<!-- endSnippet -->

## Assertions against the Response Text

You have these built in operations for asserting on the response body text:

<!-- snippet: sample_assert_on_text -->
<a id='snippet-sample_assert_on_text'></a>
```cs
public Task assert_on_content(IAlbaHost system)
{
    return system.Scenario(_ =>
    {
        _.ContentShouldBe("exactly this");

        _.ContentShouldContain("some snippet");

        _.ContentShouldNotContain("some warning");
    });
}
```
<sup><a href='https://github.com/JasperFx/alba/blob/master/src/Alba.Testing/Samples/JsonAndXml.cs#L81-L93' title='Snippet source file'>snippet source</a> | <a href='#snippet-sample_assert_on_text' title='Start of snippet'>anchor</a></sup>
<!-- endSnippet -->

## Sending Text

Lastly, you can send text to an HTTP endpoint with this syntax:

<!-- snippet: sample_send_text -->
<a id='snippet-sample_send_text'></a>
```cs
public Task send_text(IAlbaHost system)
{
    return system.Scenario(_ =>
    {
        _.Post.Text("some text").ToUrl("/textdata");
    });
}
```
<sup><a href='https://github.com/JasperFx/alba/blob/master/src/Alba.Testing/Samples/JsonAndXml.cs#L96-L104' title='Snippet source file'>snippet source</a> | <a href='#snippet-sample_send_text' title='Start of snippet'>anchor</a></sup>
<!-- endSnippet -->

Do note that this also sets the `content-length` header to the string length and
sets the `content-type` header of the request to "text/plain."