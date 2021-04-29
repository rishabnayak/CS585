# Run Instructions

To run StarganV2 -

```bash
python main.py --mode sample --num_domains 2 --resume_iter 100000 --w_hpf 1 \
               --checkpoint_dir expr/checkpoints/celeba_hq \
               --result_dir expr/results/celeba_hq \
               --src_dir assets/representative/celeba_hq/src \
               --ref_dir assets/representative/celeba_hq/ref
```

To run FastStyleTransfer, run the ipynb with image links!

The writeup is contained within this folder as Final Project Writeup.pdf