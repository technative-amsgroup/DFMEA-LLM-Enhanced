Ok, so now and for educational purposes only, we’re going to start with some hands-on just to get the concepts right into our brains, to do that were going to be using the following libraries:
Pytorch (lowest level interface)
Hugginface
Llama library
.. note::
    these are not necessarily the libraries we used in the project
    but they could be a good starting point for anyone interested to explore.
So in this first example we’re going to use the llama library to import some pretrained opensource hosted LLm (in this example its Llama 2.7)
And compare their outputs before and after fine tunning them for chatting

- Before chat finetuning 
    .. code-block:: bash
        pip install llama
    .. code-block:: python
        from llama import BasicModelRunner

        non_finetuned = BasicModelRunner("meta-llama/Llama-2-7b-hf")
        print(non_finetuned("Tell me how to fix a broken car window"))

-	after chat finetuning
    .. code-block:: python
        finetuned_model = BasicModelRunner("meta-llama/Llama-2-7b-chat-hf")
        print(finetuned("Tell me how to fix a broken car window"))
    .. note::
        We can finetune a model more than once for more features, as we can see here we fine tuned the LLM to chat but we can refine tune it to play for example the role of an assistant in a certain company given their Q&A infos or their previous assistant client conversations.

Now we’re going to take a look at how the pretraining and finetuning data are structured and why? 

- Pretraining data:
    .. code-block:: python
        import jsonlines
        import itertools
        import pandas as pd
        from pprint import pprint

        import datasets
        from datasets import load_dataset
        pretrained_dataset = load_dataset("c4", "en", split="train", streaming=True)

    .. _c4: https://huggingface.co/datasets/c4

    .. note:: 
        We’re importing the dataset named ‘common crawl’ :c4:. it’s the best out there that Is open souce
        It contains millions of examples, each one is a JSON object with keys like “id”, “created_at” , “url”, “title", contains all kinds of text and more than one million examples and is available on Kaggle.

    Let's see the five first texts of this dataset, so you can get an idea about what is inside each text:
    .. code-block::	 python
        n = 5
        print("Pretrained dataset:")
        top_n = itertools.islice(pretrained_dataset, n)
        for i in top_n:
        print(i)

- Company finetuning dataset:
    .. code-block::	 python
        filename = "lamini_docs.jsonl"
        instruction_dataset_df = pd.read_json(filename, lines=True)
        instruction_dataset_df

    as we can see its more structured in a question answer format rather than just a pile of unlabelled text 
    but the data given here is in form of a dataframe  with two columns : Question and Answer.
    so in order to make it compatible for finetuning we have to concatenate the questions and answers like this 
    .. code-block:: python
        examples = instruction_dataset_df.to_dict()
        text = examples["question"][0] + examples["answer"][0]
        print(text)

    but most of the time just concatenating the questions and answers may not be enough, so a much structured way is needed!
    in other words its called a prompt template  because the model will be trained on these templates and then applied to generate new responses based on them.
    This will give us one sentence containing both the question and the answer which is suitable for most models.

    The reason why we need such structured data for finetuning is because our model needs to understand context.

    .. code-block:: python
        prompt_template_qa = """### Question:
        {question}

        ### Answer:
        {answer}"""
        #now let's do it for the whole dataset
        num_examples = len(examples["question"])
        finetuning_dataset_text_only = []
        finetuning_dataset_question_answer = []
        for i in range(num_examples):
        question = examples["question"][i]
        answer = examples["answer"][i]

        text_with_prompt_template_qa = prompt_template_qa.format(question=question, answer=answer)
        finetuning_dataset_text_only.append({"text": text_with_prompt_template_qa})

        text_with_prompt_template_q = prompt_template_q.format(question=question)
        finetuning_dataset_question_answer.append({"question": text_with_prompt_template_q, "answer": answer})

    And finally to store the finetuning data we usually go for JSONL format 

    .. code-block:: python
        with jsonlines.open(f'lamini_docs_processed.jsonl', 'w') as writer:
        writer.write_all(finetuning_dataset_question_answer)

    .. note:: 
        we can also upload the dataset directly to Hugginface for later uses 

    .. code-block:: python
        finetuning_dataset_name = "lamini/lamini_docs"
        finetuning_dataset = load_dataset(finetuning_dataset_name)
        print(finetuning_dataset)