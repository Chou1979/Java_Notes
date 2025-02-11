
# 这是什么？
<%tp.ai.chat("用三句话总结一下这个概念的定义，尽可能注明出处：" + tp.file.title)%>

# 这对我有什么用？


# 我什么时候记的这件事？

这个文档的创建时间是：<% tp.file.creation_date()%>

<% await tp.file.move("/1. 知识文件/" + tp.file.title) %>
