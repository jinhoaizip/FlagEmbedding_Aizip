MIRACL
======

`MIRACL <https://project-miracl.github.io/>`_ (Multilingual Information Retrieval Across a Continuum of Languages) 
is an WSDM 2023 Cup challenge that focuses on search across 18 different languages.
They release a multilingual retrieval dataset containing the train and dev set for 16 "known languages" and only dev set for 2 "surprise languages".
The topics are generated by native speakers of each language, who also label the relevance between the topics and a given document list.
You can found the `dataset <https://huggingface.co/datasets/miracl/miracl-corpus>`_ on HuggingFace.

You can evaluate model's performance on MIRACL simply by running our provided shell script:

.. code:: bash

    chmod +x /examples/evaluation/miracl/eval_miracl.sh
    ./examples/evaluation/miracl/eval_miracl.sh

Or by running:

.. code:: bash

    python -m FlagEmbedding_Aizip.evaluation.miracl \
    --eval_name miracl \
    --dataset_dir ./miracl/data \
    --dataset_names bn hi sw te th yo \
    --splits dev \
    --corpus_embd_save_dir ./miracl/corpus_embd \
    --output_dir ./miracl/search_results \
    --search_top_k 1000 \
    --rerank_top_k 100 \
    --cache_path /root/.cache/huggingface/hub \
    --overwrite False \
    --k_values 10 100 \
    --eval_output_method markdown \
    --eval_output_path ./miracl/miracl_eval_results.md \
    --eval_metrics ndcg_at_10 recall_at_100 \
    --embedder_name_or_path BAAI/bge-m3 \
    --reranker_name_or_path BAAI/bge-reranker-v2-m3 \
    --devices cuda:0 cuda:1 \
    --cache_dir /root/.cache/huggingface/hub \
    --reranker_max_length 1024

change the embedder, reranker, devices and cache directory to your preference.

.. toctree::
   :hidden:

   miracl/data_loader
   miracl/runner